---
layout: post
title: "Kotlin Basics"
date: 2023-09-14 20:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: kotlin-basics
categories: [kotlin]
tags: [kotlin]
published: false
---
The Kotlin programming language is a modern language that provides you with more power for your everyday tasks. Kotlin is concise, safe, pragmatic, and focused on interoperability with Java code.
It can be used almost everywhere Java is used today for server-side development, Android apps, and much more.
Kotlin class/file extension is kt. No need to put semicolon to the end of the code lines.

Intellij Idea can convert your code from Java to Kotlin. This is a vital feature for Java developers to learn Kotlin.

<img src="/assets/images/kotlin-basics.png" />

---

### Variable Definitions
```kotlin
package hello
fun main() {
    var string: String  = "Hello, World!"  // defining a variable
    println("$string")
}
```

You can convert from Java code to Kotlin. Kotlin code can be converted to Java byte code.
- Java source code -> .java
- Kotlin source code -> .kt
- Java byte code -> .class

> .kt -> .class like .java -> .class
---

### Class Definitions
- Person class in Java
```java
class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
      this.name = name;
      this.age = age;
    }

    public String getName() {
      return name;
    }

    public int getAge() {
      return age;
    }
}
```
- Person class in Kotlin
```kotlin
data class Person(val name: String, val age: Int)
// data includes equals, hashCode, toString
```
---

### Converting usages of the Person class

- Java writing style to be used writing the name of the person to the console.
```java
Person person = new Person("Alice",27);
System.out.println(person.getName());
```
- Kotlin way
```kotlin
val person = Person("Alice",27)
println(person.name)
```

---

### Switch-case Statements

- updateWeather function in Java
```java
public void updateWeather (int degress) {
    String description;
    Color color;
    if(degrees < 10) {
      description="cold";
      color = BLUE;
    } else if(degrees < 25) {
      description="cold";
      color = ORANGE;
    } else {
      description="hot";
      color = RED;
    }
}
```

> You can create an object without using `new` keyword in Kotlin. <br />
`new Abc(description, color)}` => `Abc("cold", BLUE)`

- updateWeather function in Kotlin
```kotlin
  fun updateWeather(degrees: Int) {
    val (description, color) = when {
        degrees < 10 -> "cold" to BLUE
        degrees < 25 -> "mild" to ORANGE
        else -> "hot" to RED
    }
  }
```
---
### Passing parameters
```kotlin
fun main(args: Array<String>) {
    println("Hello, ${args.getOrNull(0)}!")
}
```
```console
Hello, null!
Hello, Kotlin!
```
---
### val / var usage

- `val` -> read-only like a final variable immutable. read-only reference, not object
  ```kotlin
  val mutableList = mutableListOf("Java")
  mutableList.add("Kotlin")
  ```
  MutableList refers to an object in memory. We can't assign another reference to the mutableList variable, but we can easily modify the exact object.

  Since you cannot modify a read-only list, the following lines of code is not going to be compiled.
  ```kotlin
  val readOnlyList = listOf("Java")
  readOnlyList.add("Kotlin") // doesn't compile
  ```
  By default, strive to declare all your new variables with 'val' keyword, not 'var'. Prefer val to var. Using immutable references, immutable objects and functions without side effects makes your code closer to the functional style, which is easier to understand and support in the end.

- `var` -> mutable. Local type inference.
  As you can see below, you can define variables in both ways. If you have assigned value, there is no need to specify the type of variable.
  ```kotlin
  val greeting : String = "Hi!"
  var number: Int = 0
  ```
  ```kotlin
  val greeting = "Hi!"
  var number = 0
  ```
  Compilation error because you can't assign a string literal to a variable of Int type
  ```kotlin
  var string = 1
  string = "abc"
  ```
---
I've tried to explain the basics of Kotlin language. In the next section, I will present examples of functions.
