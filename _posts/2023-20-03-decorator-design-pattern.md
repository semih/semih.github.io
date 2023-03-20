---
layout: post
title: "Decorator Design Pattern"
date: 2023-03-20 20:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: decorator-design-pattern
categories: [design-patterns]
tags: [design-patterns]
published: true
---
**Decorator Design Pattern** is used for adding new behaviours to objects either statically or dynamically without affecting the behavior of other objects from the same class.

- We can extend object's behaviour **without making a new subclass**.
- We can **add or remove responsibilities** from an object at runtime.
- We can **combine several behaviours** to an object.

I will explain the purpose of the Decorator pattern in detail so that we might use it correctly.

**Purpose:** The decorator design pattern is used to add new functionality to an existing object without changing its structure.
It is often used when the desired behavior cannot be achieved through interface or when you want to add behavior to an object at runtime.
---
There are several key points to implement the decorator pattern.
It involves creating a decorator class that wraps around the original object and adds new behavior to it. The decorator class has the same interface as the original object, so it can be used in the same way.
You can wrap a component with any number of decorators.

The decorator pattern consists of four components:
1. **Component Interface** (defines the methods that will be implemented by the concrete component and any decorators.)
2. **Concrete Component** (is the original object that the decorator will add new behavior to.)
3. **Decorator Abstract Class** (is an abstract class that implements the component interface and contains a reference to the original object.)
4. **Concrete Decorator** (is a subclass of the decorator abstract class that adds new behavior to the original object.)

I'm going to continue the article with encoding and compression decorators example.
There is going to be a class could only read and write data in plain text. Then we are going to create several wrapper classes.

The first wrapper encrypts and decrypts data, and the second one compresses and extracts data. You can also combine these wrappers by one decorator with another.
<img src="/assets/images/design-patterns-decorator.jpeg" width="1400" />

Let's take a look at the implementation.

```java
package com.decorator;

public interface DataSource {
  void writeData(String data);
  String readData();
}
```

```java
package com.decorator;

public class FileDataSource implements DataSource {
  private String name;
  public FileDataSource(String name) {
    this.name = name;
  }
  @Override
  public void writeData(String data) {
    System.out.println(data + "is written.");
  }

  @Override
  public String readData() {
    return "read data";
  }
}
```

```java
package com.decorator;

public class DataSourceDecorator implements DataSource {
    private DataSource wrappee;

    DataSourceDecorator(DataSource source) {
        this.wrappee = source;
    }

    @Override
    public void writeData(String data) {
        wrappee.writeData(data);
    }

    @Override
    public String readData() {
        return wrappee.readData();
    }
}
```

```java
package com.decorator;

public class EncryptionDecorator extends DataSourceDecorator {

  public EncryptionDecorator(DataSource source) {
    super(source);
  }

  @Override
  public void writeData(String data) {
    super.writeData(encode(data));
  }

  @Override
  public String readData() {
    return decode(super.readData());
  }

  private String encode(String data) {
    return data + " is encoded";
  }

  private String decode(String data) {
    return data + " is decoded";
  }
}
```

```java
package com.decorator;

public class CompressionDecorator extends DataSourceDecorator {
  public CompressionDecorator(DataSource source) {
    super(source);
  }

  @Override
  public void writeData(String data) {
    super.writeData(compress(data));
  }

  @Override
  public String readData() {
    return decompress(super.readData());
  }

  private String compress(String stringData) {
    return stringData + " is compressed.";
  }

  private String decompress(String stringData) {
    return stringData + " is decompressed.";
  }
}
```

```java
package com.decorator;

public class Demo {
  public static void main(String[] args) {
    String salaryRecords = "Name,Salary\nJohn Smith,100000\nSteven Jobs,912000";

    DataSourceDecorator encoded = new CompressionDecorator(
      new EncryptionDecorator(
        new FileDataSource("OutputDemo.txt")));
    encoded.writeData(salaryRecords);

    DataSource plain = new FileDataSource("OutputDemo.txt");

    System.out.println("- Input ----------------");
    System.out.println(salaryRecords);
    System.out.println("- Encoded --------------");
    System.out.println(plain.readData());
    System.out.println("- Decoded --------------");
    System.out.println(encoded.readData());
  }
}
```

Here are the results.
```bash
Name,Salary
John Smith,100000
Steven Jobs,912000 is compressed. is encodedis written.
- Input ----------------
Name,Salary
John Smith,100000
Steven Jobs,912000
- Encoded --------------
read data
- Decoded --------------
read data is decoded is decompressed.

Process finished with exit code 0
```

To summarize, a decorator can be recognized by methods or constructors that accept objects of the same type.
You can see the examples of decorator classes in core Java libraries.
`java.io.InputStream, OutputStream, Reader` and `Writer` have constructors that accept objects of their own type.
