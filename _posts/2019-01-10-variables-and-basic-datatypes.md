---
layout: post
title: "Variables and Basic DataTypes"
date: 2019-01-10 23:00:00 Wednesday
author: semih
comments: true
lang: en
lang-ref: data-types
categories: [java]
tags: [java, datatypes]
published: true
---
Although Java is object oriented, not all types are object. There are primitive types as well. Here is a list of all primitive types in Java:
<br/>

### Primitive Datatypes:
<div class="datatable-begin"></div>

Data Type    | Description                           | Size | Example Literals | Range
------- | ------------------------------------- | -------- | ----------- | -----------
byte		| twos complement integer  | 8 bits   | (none) | -2^7...2^7-1
short		| twos complement integer  | 16 bits  | (none) | -2^15...2^15-1
int			| twos complement integer  | 32 bits  | -2, -1, 0, 1, 2 | -2^31...2^31-1
long		| twos complement integer  | 64 bits  | -2L, -1L, 0L, 1L, 2L | -2^63...2^63-1
float  	| IEEE 754 floating point  | 32 bits  | 1.23e100f, -1.23e-100f, .3f, 3.14F | 
double 	| IEEE 754 floating point  | 64 bits  | 1.23456e300d, -1.23456e-300d, 1e1d | 
boolean   | true or false            | 1 bit    | true, false | 0...1
char 		| Unicode character        | 16 bits  | 'a', '\u0041', '\101', '\\', '\'', '\n', 'ß' | '\u0000'...'\uffff' or 0...65,535 inclusive

<div class="datatable-end"></div>
<br/>
### Reference Datatypes:

Data Type    | Description                           | Size | Example Literals | Range
------- | ------------------------------------- | -------- | ----------- | -----------
Class objects and various type of array variables | These variables are declared to be of a specific type that cannot be changed | - | Animal animal = new Animal(giraffe); | -

_**Numbers**_

```java
byte a = 68;
int myNumber = 5;
double d = 4.5;
float f = (float) 4.5;
float f = 4.5f; // (f is a shorter way of casting float)
```

_**Characters and Strings**_

```java
char c = 'g';
```

Double quotes automatically creates a new String object.
String objects are immutable, which means that once created, their values cannot be changed.
<br/>For example: `String s = "this is a string";`


```java
String s1 = new String("Who let the dogs out?"); // String object stored in heap memory
String s2 = "Who who who who!";	// String literal stored in String pool
```

_**Boolean**_

```java
boolean b = false;
```

Hope to see you in the next article...