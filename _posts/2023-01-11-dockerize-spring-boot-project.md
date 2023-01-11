---
layout: post
title: "Dockerize Spring Boot Project"
date: 2023-01-10 23:00:00 Wednesday
author: semih
comments: true
lang: en
lang-ref: docker
categories: [Introduction to Java]
tags: [java, docker, container]
published: true
---
In this article, we will learn how to create a composition of containers.

**1. define a DockerFile in the module**

```bash
FROM openjdk:17-alpine
COPY /target/*.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]
```

**2. add maven plugin as a plugin**
```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

**3. define a bitbucket-pipelines(optional)**

**4. execute java jar command**
   
java -jar target/account-service-1.0.0.jar

```bash
docker ps -a
docker rm f883019f5835   
docker ps -a    
docker images      
docker rmi a67aecce36a5
```

**5. run docker build commands**

```bash
docker build -t company-example-service .
docker run -p 8085:8085 --name company-example-service -d company-example-service
docker run -p 8085:8085 -e PORT=8085 -e POSTGRESQL_HOST=192.168.X.X -e POSTGRESQL_PORT=5432 -e POSTGRESQL_DB_NAME=exampleDb -e POSTGRESQL_USER=postgres -e POSTGRESQL_PASSWORD=postgres --name company-example-service -d company-example-service

docker ps -a      
docker logs -f 904957ee3ae2
```

I hope the information in this article is useful and enough for you. Please contact me if you have any questions or comments.