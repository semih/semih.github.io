---
layout: post
title: "What Really Happens in Spring Boot Auto-Configuration"
date: 2025-08-03 22:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: spring-boot-auto-configuration
categories: [spring-boot]
tags: [springboot, java, autoconfiguration]
published: true
---

<img src="/assets/images/spring-boot-auto-configuration.jpg" width="500" />

## Introduction

Spring Boot follows the idea of using smart defaults instead of requiring a lot of setup. One of its most powerful features is **auto-configuration**, which automatically sets up components based on your project setup.

In this article, we'll uncover how auto-configuration works, how Spring Boot decides which beans to register, how to override default behavior, and a few important nuances that even experienced developers often overlook.

## What Is Auto-Configuration?

Auto-configuration is the mechanism by which Spring Boot automatically configures beans in the `ApplicationContext` based on:

* What's on the classpath
* Application properties
* Existing user-defined beans
* Metadata declarations in `META-INF`

It eliminates most boilerplate configurations and helps you get started faster.

## How Auto-Configuration Works: 3 Main Steps

### 1. Classpath Scanning

Spring Boot scans the project's dependencies (classpath) to check for specific libraries or classes. Based on what it finds, it determines which components should be configured.

For example:

* Adding `spring-boot-starter-data-jpa` brings in a JDBC driver and JPA classes, so Spring Boot tries to configure a `DataSource` bean.
* Adding `spring-boot-starter-web` triggers the creation of `DispatcherServlet` and embedded web server beans.

> _Spring Boot uses the `@ConditionalOnClass` annotation to apply a configuration only when a specific class is present on the classpath._

### 2. The Role of `META-INF` Files

Spring Boot uses special files inside its jars to locate auto-configuration classes:

* **Before Spring Boot 2.7:** `META-INF/spring.factories` listed all auto-config classes.
* **Starting Spring Boot 2.7+:** `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` replaced the old file for better modularity.

These files contain fully qualified names of auto-configuration classes. Spring Boot reads these files during startup to load potential configurations.

### 3. Conditional Configuration with Annotations

Once candidate configuration classes are loaded, Spring Boot uses conditional annotations to decide which to activate:

* `@ConditionalOnClass`: Checks if a specific class is present on the classpath
* `@ConditionalOnMissingBean`: Avoids creating a bean if one already exists
* `@ConditionalOnProperty`: Activates config only if a specific property is set

For example:

`DataSourceAutoConfiguration` activates only if:

* The `javax.sql.DataSource` class is on the classpath (`@ConditionalOnClass`)
* The property `spring.datasource.url` is defined (`@ConditionalOnProperty`)

```java
@Configuration
@ConditionalOnClass(javax.sql.DataSource.class)
@ConditionalOnProperty(prefix = "spring.datasource", name = "url")
public class DataSourceAutoConfiguration {
    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource dataSource() {
        return DataSourceBuilder.create().build();
    }
}
```

## How Spring Boot Applies Auto-Configuration

The process includes:

1. **Enabling Auto-Configuration:**  
`@EnableAutoConfiguration` or `@SpringBootApplication` triggers Spring Boot to start processing auto-config classes listed in the `AutoConfiguration.imports` file.
2. **Loading Configuration Classes:**  
 Spring Boot loads all candidate configuration classes declared in metadata files.
3. **Evaluating Conditions:**  
 Each configuration class's conditional annotations are evaluated against the current runtime environment.
4. **Registering Beans:**  
 Beans from configurations whose conditions pass are registered into the application context.

## Are Auto-Configuration Classes Dynamic?

A key point often misunderstood:

> Auto-configuration classes are static and do not change their code based on your dependencies.

Their source code — like `DataSourceAutoConfiguration` — is fixed inside the Spring Boot jars.

What changes is whether Spring Boot **activates** these classes based on conditions such as classpath contents and properties.

### So, What _Does_ Change?

* Which dependencies are available on the classpath
* What properties are defined in `application.properties` or `application.yaml`

For example The `DataSourceAutoConfiguration` class is **always available** in Spring Boot. But if `javax.sql.DataSource` is **not present** on the classpath or if `spring.datasource.url` is **not configured** in your properties. Then Spring Boot will simply **skip** this configuration — it won't run the code inside `DataSourceAutoConfiguration` and won't create any related beans.

## Dynamic Bean Configuration in Action

Spring Boot dynamically creates beans based on runtime data such as:

* Dependencies found on classpath
* Defined properties in `application.properties` or `application.yml`
* Beans already defined by the developer

Example — DataSource creation:

```java
@Component
@ConfigurationProperties(prefix = "spring.datasource")
public class DataSourceProperties {
    private String url;
    private String username;
    private String password;
    private String driverClassName;
    // getters and setters
}

@Bean
public DataSource dataSource(DataSourceProperties properties) {
    HikariDataSource dataSource = new HikariDataSource();
    dataSource.setJdbcUrl(properties.getUrl());
    dataSource.setUsername(properties.getUsername());
    dataSource.setPassword(properties.getPassword());
    dataSource.setDriverClassName(properties.getDriverClassName());
    return dataSource;
}
```

## Overriding and Excluding Auto-Configuration

### Excluding Auto-Configurations

You can exclude auto-configuration classes to prevent Spring Boot from applying them:

* Via annotation:

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
```

* Via configuration files:

```properties
# application.properties
spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

```yaml
# application.yaml
spring:
  autoconfigure:
    exclude: org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
```

Multiple exclusions supported:

```yaml
spring:
  autoconfigure:
    exclude:
      - org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration
      - org.springframework.boot.autoconfigure.web.servlet.WebMvcAutoConfiguration
```

### Defining Custom Beans

You can provide your own beans to override the auto-configured ones:

```java
@Bean
public DataSource myCustomDataSource() {
    return new HikariDataSource();
}
```

## Handling Missing Beans and Fallbacks

The code demonstrates how to provide a fallback bean when a required bean is missing. In this case, it's about the `DataSource` bean, which is used for database connections.

If no `DataSource` is defined in the application context, the application might fail to start. To prevent this, the `@ConditionalOnMissingBean` annotation is used to define a default `DataSource`.

```java
@Configuration
public class FallbackConfiguration {
    @Bean
    @ConditionalOnMissingBean(DataSource.class)
    public DataSource fallbackDataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.H2)
            .build();
    }
}
```

## Conclusion

Spring Boot's auto-configuration dramatically simplifies application setup by dynamically applying configurations based on your project's dependencies and properties.

Understanding this process empowers you to customize or disable configurations, provide your own beans, debug startup issues related to bean creation. Auto-configuration does a lot behind the scenes — now that you understand how it works, you can take full advantage of it and customize when needed.

---

*Originally published on [Medium](https://semihkirdinli.medium.com/what-really-happens-in-spring-boot-auto-configuration-c2980a8c2f28)*
