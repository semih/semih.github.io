---
layout: post
title: "Değişkenler ve Temel Veri Tipleri"
date: 2019-01-10 23:00:00 Wednesday
author: semih
comments: true
lang: tr
lang-ref: data-types
categories: [java]
tags: [java, datatypes]
---
Java, nesne yönelimli bir programlama dili olmasına rağmen tüm tipler object değildir. İlkel veri tipleri de mevcuttur. Java'da ilkel veri tiplerinin listesi aşağıdaki şekildedir:
<br/>

### İlkel Veri Tipleri:
<div class="datatable-begin"></div>

Veri Tipi    | Açıklama                          | Uzunluk | Örnek | Değer Aralığı
------- | ------------------------------------- | -------- | ----------- | -----------
byte		| iki tümleyeni integer  | 8 bit   | (none) | -2^7...2^7-1
short		| iki tümleyeni integer  | 16 bit  | (none) | -2^15...2^15-1
int			| iki tümleyeni integer  | 32 bit  | -2, -1, 0, 1, 2 | -2^31...2^31-1
long		| iki tümleyeni integer  | 64 bit  | -2L, -1L, 0L, 1L, 2L | -2^63...2^63-1
float  	| IEEE 754 kayan nokta  | 32 bit  | 1.23e100f, -1.23e-100f, .3f, 3.14F | 
double 	| IEEE 754 kayan nokta  | 64 bit  | 1.23456e300d, -1.23456e-300d, 1e1d | 
boolean   | true veya false            | 1 bit    | true, false | 0...1
char 		| Unicode karakterler        | 16 bit  | 'a', '\u0041', '\101', '\\', '\'', '\n', 'ß' | '\u0000'...'\uffff' or 0...65,535 dahil

<div class="datatable-end"></div>
<br/>
### Referans Veri Tipleri:

Veri Tipi    | Açıklama                           | Uzunluk | Örnek | Değer Aralığı
------- | ------------------------------------- | -------- | ----------- | -----------
Sınıf nesneleri ve dizi değişkenlerinin çeşitleri | Bu değişkenler değiştirilemeyen veri tipleri olarak tanımlanır | - | Animal animal = new Animal(giraffe); | -

_**Sayılar**_

```java
byte a = 68;
int myNumber = 5;
double d = 4.5;
float f = (float) 4.5;
float f = 4.5f;						// (f is a shorter way of casting float)
```

_**Karakter Katarları ve String İfadeler**_

```java
char c = 'g';
```

Çift tırnak, otomatik olarak String tipinde bir nesne yaratır.
String nesnelerinin değerleri, bir kere yaratıldıktan sonra değiştirilemez.
<br/>Örnek: `String s = "this is a string";`


```java
String s1 = new String("Who let the dogs out?");	// String object stored in heap memory
String s2 = "Who who who who!";				// String literal stored in String pool
```

_**Boolean İfadeler**_

```java
boolean b = false;
```

Bir sonraki makalede görüşmek üzere...