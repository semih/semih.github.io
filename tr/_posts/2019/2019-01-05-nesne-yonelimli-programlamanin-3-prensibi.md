---
layout: post
title: "Değişkenler ve Temel Veri Tipleri"
date: 2019-01-05 23:00:00 Wednesday
author: semih
comments: true
lang: tr
lang-ref: data-types
categories: [java]
tags: [java, oop]
---
Nesne yönelimli programlama(object oriented programming - oop) Java'nın temelidir. Tüm nesne yönelimli programlama dilleri, nesne yönelimli modeli uygularken size yardımcı olan mekanizmaları içerir. Bunlar sarmalama(encapsulation), kalıtım(inheritance) ve çok biçimliliktir(polymorphism). Bu kavramlara göz atalım.
<br/>

### Encapsulation
Bu özellik, dilin nesne kullanıcısından gereksiz uygulama ayrıntılarını saklar. Oluşturulan bir sınıf (class) içerisinde kullanıcının işlemlerini daha kolay gerçekleştirebilmesi için bazı işlemler birleştirilerek tek bir işlem gibi gösterilir. Bu birleştirme işlemine encapsulation denir.
<br/>
Erişim belirteçleri (access modifier) sayesinde kapsülleme çok daha kolay yapılmaktadır. Erişim belirteçleri, oluşturulan sınıf veya sınıf içindeki elemanların erişim seviyelerini belirlemek için kullanılan anahtar kelimeler grubuna verilen isimdir. Encapsulation "private" değişkenlerin metotlar gibi kullanılmasına yardımcı olur. Okuma (Read Only) işleminin yanısıra okuma - yazma (read - write) işleminin yapılmasını sağlar. Özetle sınıfı kontrolsüz değişime kapamak için kullanılır diyebiliriz. Böylelikle yanlış işlemlerin gerçekleşmeyeceğinden emin olabilirsiniz.

```java
package encapsulation;

public class Student
{
	public int Id;
	public String Name;
	public String SchoolNumber;
	private double Score; // Not alanı kapsülleniyor.

	public void SetScore(double value) {
		if (value > 0 && value<100) //set metoduyla verilen değerin uygun olması durumunda Not alanına atama yapılır
			Score = value;

		else //uygun olmaması durumunda kullanıcıya hata mesajı verilir.
			System.out.println("Score is invalid");
	}
	
	public double GetScore() {
		return Score;
	}
}
```

Program sınıfında bir Ogrenci nesnesi oluşturulup değer ataması ise şu şekilde yapılır:

```java
package encapsulation;
import java.util.Scanner;

public class Program {

	public static void main(String[] args) {
        double value; //value değişkenine atama yapılmalıdır. Bu haliyle uygulama hata verecektir.
        Student student = new Student();
        
        Scanner scanner = new Scanner(System.in);
        value = scanner.nextDouble();
        o.SetScore(value);
        System.out.print(o.GetScore());
	}
}
```

<br/>
### Referans Veri Tipleri:



Bir sonraki makalede görüşmek üzere...