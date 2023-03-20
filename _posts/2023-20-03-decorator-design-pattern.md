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

import java.io.File;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.IOException;
import java.io.OutputStream;

public class FileDataSource implements DataSource {
  private String name;
  public FileDataSource(String name) {
    this.name = name;
  }
  @Override
  public void writeData(String data) {
    File file = new File(name);
    try (OutputStream fos = new FileOutputStream(file)) {
      fos.write(data.getBytes(), 0, data.length());
    } catch (IOException ex) {
      System.out.println(ex.getMessage());
    }
  }

  @Override
  public String readData() {
    char[] buffer = null;
    File file = new File(name);
    try (FileReader reader = new FileReader(file)) {
      buffer = new char[(int) file.length()];
      reader.read(buffer);
    } catch (IOException ex) {
      System.out.println(ex.getMessage());
    }
    return new String(buffer);
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

import java.util.Base64;

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
    byte[] result = data.getBytes();
    for (int i = 0; i < result.length; i++) {
      result[i] += (byte) 1;
    }
    return Base64.getEncoder().encodeToString(result);
  }

  private String decode(String data) {
    byte[] result = Base64.getDecoder().decode(data);
    for (int i = 0; i < result.length; i++) {
      result[i] -= (byte) 1;
    }
    return new String(result);
  }
}
```

```java
package com.decorator;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.Base64;
import java.util.zip.Deflater;
import java.util.zip.DeflaterOutputStream;
import java.util.zip.InflaterInputStream;

public class CompressionDecorator extends DataSourceDecorator {
  private int compLevel = 6;

  public CompressionDecorator(DataSource source) {
    super(source);
  }

  public int getCompressionLevel() {
    return compLevel;
  }

  public void setCompressionLevel(int value) {
    compLevel = value;
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
    byte[] data = stringData.getBytes();
    try {
      ByteArrayOutputStream bout = new ByteArrayOutputStream(512);
      DeflaterOutputStream dos = new DeflaterOutputStream(bout, new Deflater(compLevel));
      dos.write(data);
      dos.close();
      bout.close();
      return Base64.getEncoder().encodeToString(bout.toByteArray());
    } catch (IOException ex) {
      return null;
    }
  }

  private String decompress(String stringData) {
    byte[] data = Base64.getDecoder().decode(stringData);
    try {
      InputStream in = new ByteArrayInputStream(data);
      InflaterInputStream iin = new InflaterInputStream(in);
      ByteArrayOutputStream bout = new ByteArrayOutputStream(512);
      int b;
      while ((b = iin.read()) != -1) {
        bout.write(b);
      }
      in.close();
      iin.close();
      bout.close();
      return new String(bout.toByteArray());
    } catch (IOException ex) {
      return null;
    }
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
- Input ----------------
Name,Salary
John Smith,100000
Steven Jobs,912000
- Encoded --------------
Zkt7e1Q5eU8yUm1Qe0ZsdHJ2VXp6dDBKVnhrUHtUe0sxRUYxQkJIdjVLTVZ0dVI5Q2IwOXFISmVUMU5rcENCQmdxRlByaD4+
- Decoded --------------
Name,Salary
John Smith,100000
Steven Jobs,912000

Process finished with exit code 0
```

To summarize, a decorator can be recognized by methods or constructors that accept objects of the same type.
You can see the examples of decorator classes in core Java libraries.
`java.io.InputStream, OutputStream, Reader` and `Writer` have constructors that accept objects of their own type.
