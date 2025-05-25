---
layout: post
title: "Kotlin Functions"
date: 2023-09-18 20:00:00 +0300
author: semih
comments: true
lang: en
lang-ref: kotlin-functions
categories: [kotlin]
tags: [kotlin]
published: false
---
In this section, you will learn the different syntax of how to define a function in Kotlin. To create your own function, use the `fun` keyword, and write the function name, followed by parentheses.
You can use predefined functions, create your own functions, or call a function.

### Predefined Functions
```kotlin
fun main() {
  println("Hello World")
}
```
### Create Your Own Functions
```kotlin
fun myFunction() {
  println("I am learning Kotlin functions.")
}
```
### Call a Function
```kotlin
fun main() {
  myFunction()
}
```
### Function Parameters
```kotlin
fun myFunction(fname: String) {
  println(fname + " Doe")
}
```
### Return Values
```kotlin
fun max(a: Int, b: Int): Int {
  return if(a > b) a else b
}
```
Shorter syntax for return values.
```kotlin
fun max(a: Int, b: Int): Int = if(a > b) a else b
```
If you try to omit the type for a function with expression body, it will mean that this function returns `Unit`. You can consider of `Unit` as `void` in Java.
```kotlin
fun displayMax(a: Int, b: Int) = println(max(a, b))
// An equivalent syntactic form
fun displayMax(a: Int, b: Int): Unit = println(max(a, b))
```

### Kotlin Function Types
In Kotlin, you can define functions everywhere. You can define a function at the  top-level or make it a member of a class.
You can even define function inside another function, then it's called a local function.
#### ___Top-level function___
```kotlin
fun topLevel() = 1
```
You call it as a static function of the class, which name corresponds to the file name.
> `@JVMName` changes the JVM name of the class containing top-level functions.
> ```kotlin
> // Extension.kt
> @file:JvmName("Util")
> package intro
> fun foo() = 0
> // It is used from Java like Util.foo()
> ```

#### ___Member function___
```kotlin
class A {
    fun member() = 2
}
```
#### ___Local function___
```kotlin
fun other() {
    fun local() = 3
}
```

### Named & Default Arguments
```kotlin
println(listOf('a','b','c').joinToString(separator = "", prefix = "(", postfix = ")"))
// output is (abc)
println(listOf('a','b','c').joinToString(postfix = "."))
// output is a,b,c. (default separator is comma ,)
```

You can either provide another value or use a default one.
```kotlin
fun displaySeparator(character: Char = '*', size: Int = 10) {
    repeat(size){
        print(character)
    }
}

displaySeparator('#', 5)                        // #####
displaySeparator('#')                           // ##########
displaySeparator()                              // **********
displaySeparator(size = 5)                      // *****
displaySeparator(size = 3, character = '5')     // 555
```
I've tried to explain the functions in Kotlin language. I will present examples about control structures.
