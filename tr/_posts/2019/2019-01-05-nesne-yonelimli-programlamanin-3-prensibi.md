---
layout: post
title: "Nesne Yönelimli Programlamanın 3 Prensibi"
date: 2019-01-05 23:00:00 Wednesday
author: semih
comments: true
lang: tr
lang-ref: data-types
categories: [java]
tags: [java, oop, encapsulation, inheritance, polymorphism, abstraction, immutable]
---
Nesne yönelimli programlama(object oriented programming - oop) Java'nın temelidir. Tüm nesne yönelimli programlama dilleri, nesne yönelimli modeli uygularken size yardımcı olan mekanizmaları içerir. Bunlar sarmalama(encapsulation), kalıtım(inheritance) ve çok biçimliliktir(polymorphism). Bu kavramlara göz atalım.
<br />
### Sarmalama (Encapsulation)
Bu özellik, dilin nesne kullanıcısından gereksiz uygulama ayrıntılarını saklar. Oluşturulan bir sınıf (class) içinde kullanıcının işlemlerini daha kolay gerçekleştirebilmesi için bazı işlemler birleştirilerek tek bir işlem gibi gösterilir. Bu birleştirme işlemine encapsulation denir.

Erişim belirteçleri (access modifier) sayesinde kapsülleme çok daha kolay yapılmaktadır. Erişim belirteçleri, oluşturulan sınıf veya sınıf içindeki elemanların erişim seviyelerini belirlemek için kullanılan anahtar kelimeler grubuna verilen isimdir. Encapsulation "private" değişkenlerin metotlar gibi kullanılmasına yardımcı olur. Okuma (Read Only) işleminin yanısıra okuma - yazma (read - write) işleminin yapılmasını sağlar. Özetle sınıfı kontrolsüz değişime kapamak için kullanılır diyebiliriz. Böylelikle yanlış işlemlerin gerçekleşmeyeceğinden emin olabiliriz.

```java
package encapsulation;

public class Student
{
  public int id;
  public String name;
  public String schoolNumber;
  private double score; // score alanı kapsülleniyor.

  public void setScore(double value) {
    if (value > 0 && value < 100) // set metoduyla verilen değerin uygun olması durumunda score alanına atama yapılır
      score = value;

    else //uygun olmaması durumunda kullanıcıya hata mesajı verilir.
      System.out.println("score is invalid");
  }
	
  public double getScore() {
    return score;
  }
}
```

Program sınıfında bir Student nesnesi oluşturulup değer ataması ise şu şekilde yapılır:

```java
package encapsulation;
import java.util.Scanner;

class Program {
  public static void main(String[] args) {
    double value; //value değişkenine atama yapılmalıdır. Bu haliyle uygulama hata verecektir.
    Student student = new Student();
        
    Scanner scanner = new Scanner(System.in);
    value = scanner.nextDouble();
    student.setScore(value);
    System.out.print(student.GetScore());
  }
}
```
Örnekte student nesnesinin score bilgisine doğrudan değer atanmadığı görülüyor. Program.java sınıfı içinde ```student.score=value``` şeklinde atama yapılmak istendiğinde (score değişkeninin erişim belirteci private olduğundan) kod parçası hata verecektir. Bunun yerine ```student.setScore(value)``` şeklinde metot çağrılarak değer atamasının yapılması sağlanmıştır.
Setter metotlarını kaldırsaydık ve yeni bir constructor oluşturarak sınıfın içinde yer alan tüm değişkenleri bu constructor'da set etseydik, bu sınıfı kullanan istemci sadece nesne üretirken değer ataması yapabilecek, sonradan bu değerler değiştirilemeyecekti. Böyle sınıflara immutable sınıf adı verilir. Immutable olarak tasarlanan sınıflar çok kanallı programlamada thread korumalıdır(thread-safe). Değişmez sınıf nesnelerinin içerikleri değişmeyeceği için program akışı içinde içerikte istenmeyen değişikliklerin olmasının önüne geçecektir.
<br/>
### Kalıtım (Inheritance)
Kalıtım(inheritance), bir nesnenin başka bir nesnenin özelliklerini devralmasıdır. Bu, hiyerarşik sınıflandırma kavramını desteklediği için önemlidir. Örnek vermek gerekirse köpek, memeli ve hayvan sınıfları olduğunu düşünelim. Örneğin Golden, hayvanlar sınıfı altındaki memeliler sınıfının bir parçası olan köpek sınıflandırmasındadır. Hiyerarşi kullanımı olmasaydı, her bir sınıfın ihtiyacı olan tüm karakteristiklerin açıkça tanımlanması gerekirdi. Ancak kalıtımın kullanılmasıyla sadece sınıf içinde kendine has özelliklerin tanımlanması yeterli olur. Genel nitelikler üst sınıftan devralınabilir. Böylece kalıtım sayesinde bir nesne daha genel bir başka nesnenin belirli bir örneği olabilir. 

Hayvan -> Büyüklük, Zeka, İskelet Sistemi Tipi, Yerler, Nefes Alırlar, Uyurlar
Memeliler -> Diş Tipi, Meme Bezleri 

Memeliler, daha kesin olarak tanımlanmış hayvanlar olduğundan, hayvanların tüm niteliklerini devralırlar. Türetilen bir alt sınıf, sınıf hiyerarşisinde atalarının tüm niteliklerini devralır.
<br />
### Çok Biçimlilik (Polymorphism)
Birden fazla sınıfın ortak kullanacağı bir metot varsa, bu metot her bir sınıfın kalıtım alacağı ana sınıf içerisinde tanımlanabilir. Davranış şekillerindeki farklılıklar ise her sınıfın kendi yapısı içinde ifade edilir.

Bir kalıtım ağacına ait sınıflarda aynı imza (dönüş tipi, ad, parametreler) ile tanımlanmış bir metot varsa, Java ortamı çalıştırma zamanında metodun hangi sınıfa ait tanımdan çalıştırılacağını dinamik olarak belirleyebilir. Bu özelliğe çok biçimlilik(polymorphism) denir.

Aşağıdaki örnekte görüldüğü üzere 	```Animal``` ana sınıfına ait ```animalSound``` metodu çağrılıyor. Hayvan ana sınıfından domuz, kedi, köpek, kuş gibi sınıflar türetilebilir ve onlar hayvan sesini kendi içlerinde farklılaştırabilir, ```animalSound``` metoduna farklı görevler yükleyebilir. Böylece nesne yönelimli programlanın çok biçimlilik özelliği, tek bir eylemi farklı şekillerde gerçekleştirmemizi sağlar. 
<br />

```java
class Animal {
  public void animalSound() {
    System.out.println("The animal makes a sound");
  }
}

class Pig extends Animal {
  public void animalSound() {
    System.out.println("The pig says: wee wee");
  }
}

class Dog extends Animal {
  public void animalSound() {
    System.out.println("The dog says: bow wow");
  }
}

public class Program {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();  // Create a Animal object
    Animal myPig = new Pig();  // Create a Pig object
    Animal myDog = new Dog();  // Create a Dog object
    myAnimal.animalSound();
    myPig.animalSound();
    myDog.animalSound();
  }
}
```

Bir sonraki makalede görüşmek üzere...