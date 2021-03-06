---
layout: post
title: "Nesne Yönelimli Programlama'nın Temel Prensipleri"
date: 2019-01-05 23:00:00 Wednesday
author: semih
comments: truesound
lang: tr
lang-ref: data-types
categories: [java]
tags: [java, oop, encapsulation, inheritance, polymorphism, abstraction, immutable]
---
Nesne Yönelimli Programlama(Object Oriented Programming) Java'nın temelidir. Tüm nesne yönelimli programlama dilleri, nesne yönelimli modeli uygularken size yardımcı olan mekanizmaları içerir. 

Nesne Yönelimli Programlama teorisinde 4 temel özelliğin gerçekleştirilmesi zorunlu sayılmıştır. Bir tanesi bile eksik olduğunda dil saf Nesne Yönelimli PProgramlama yaklaşımına uygun olmamaktadır. Bu özellikler:

* Sarmalama(Encapsulation), 
* Kalıtım(Inheritance), 
* Çok Biçimlilik(Polymorphism), 
* Soyutlama(Abstraction)

<br />
### Sarmalama(Encapsulation)
Bu özellik, dilin nesne kullanıcısından gereksiz uygulama ayrıntılarını saklar. Oluşturulan bir sınıf(class) içinde kullanıcının işlemleri daha kolay gerçekleştirebilmesi için bazı işlemler birleştirilerek tek bir işlem gibi gösterilir. Bu birleştirme işlemine <b>sarmalama(encapsulation)</b> denir.

Erişim belirteçleri(access modifier) sayesinde encapsulation çok daha kolay yapılmaktadır. Erişim belirteçleri, oluşturulan sınıf veya sınıf içindeki elemanların erişim seviyelerini belirlemek için kullanılan anahtar kelimeler grubuna verilen isimdir. Encapsulation <b>private</b> değişkenlerin metotlar gibi kullanılmasına yardımcı olur. Okuma(read only) işleminin yanısıra okuma-yazma(read-write) işleminin yapılmasını sağlar. Özetle sınıfı kontrolsüz değişime kapamak için kullanılır diyebiliriz. Böylelikle yanlış işlemlerin gerçekleşmeyeceğinden emin olabiliriz.

```java
package encapsulation;

public class Student
{
  public int id;
  public String name;
  public String schoolNumber;
  private double score;
  
  // set metoduyla uygun değer geldiğinde score alanına atama yapılır.
  public void setScore(double value) {
    if(value > 0 && value < 100)
      score = value;

    else //uygun olmaması durumunda kullanıcıya hata mesajı verilir.
      System.out.println("score is invalid");
  }
	
  public double getScore() {
    return score;
  }
}
```

Program sınıfında bir ```student``` nesnesi oluşturulup değer ataması aşağıdaki şekilde yapılır:

```java
package encapsulation;
import java.util.Scanner;

public class Program {
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
Örnekte ```student``` nesnesinin ```score``` bilgisine doğrudan değer atanmadığı görülüyor. Program.java sınıfı içinde ```student.score=value``` şeklinde atama yapılmak istendiğinde(score değişkeninin erişim belirteci private olduğundan) kod parçası hata verecektir. Bunun yerine ```student.setScore(value)``` şeklinde metot çağrılarak değer atamasının yapılması sağlanmıştır.
Setter metotlarını kaldırsaydık ve yeni bir constructor oluşturarak sınıfın içinde yer alan tüm değişkenleri bu constructor'da set etseydik, bu sınıfı kullanan istemci sadece nesne üretirken değer ataması yapabilecek, sonradan bu değerler değiştirilemeyecekti. Böyle sınıflara immutable sınıf adı verilir. Immutable olarak tasarlanan sınıflar çok kanallı programlamada thread korumalıdır(thread safe). Değişmez sınıf nesnelerinin içerikleri değişmeyeceği için program akışı içinde içerikte istenmeyen değişikliklerin olmasının önüne geçecektir.
<br/>
### Kalıtım(Inheritance)
Bir nesnenin başka bir nesnenin özelliklerini devralması olayına <b>kalıtım(inheritance)</b> denir. Bu, hiyerarşik sınıflandırma kavramını desteklediği için önemlidir. Örnek vermek gerekirse köpek, memeli ve hayvan sınıfları olduğunu düşünelim. Örneğin Golden, hayvanlar sınıfı altındaki memeliler sınıfının bir parçası olan köpek sınıflandırmasındadır. Hiyerarşi kullanımı olmasaydı, her bir sınıfın ihtiyacı olan tüm karakteristiklerin açıkça tanımlanması gerekirdi. Ancak kalıtımın kullanılmasıyla sadece sınıf içinde kendine has özelliklerin tanımlanması yeterli olur. Genel nitelikler üst sınıftan devralınabilir. Böylece kalıtım sayesinde bir nesne daha genel bir başka nesnenin belirli bir örneği olabilir. 

* <b>Hayvan</b> -> Büyüklük, Zeka, İskelet Sistemi Tipi, Yerler, Nefes Alırlar, Uyurlar
* <b>Memeliler</b> -> Diş Tipi, Meme Bezleri 

Memeliler, daha kesin olarak tanımlanmış hayvanlar olduğundan, hayvanların tüm niteliklerini devralırlar. Türetilen bir alt sınıf, sınıf hiyerarşisinde atalarının tüm niteliklerini devralır.
<br />
### Çok Biçimlilik(Polymorphism)
Birden fazla sınıfın ortak kullanacağı bir metot varsa, bu metot her bir sınıfın kalıtım alacağı ana sınıf içerisinde tanımlanabilir. Davranış şekillerindeki farklılıklar ise her sınıfın kendi yapısı içinde ifade edilir.

Bir kalıtım ağacına ait sınıflarda aynı imza(dönüş tipi, ad, parametreler) ile tanımlanmış bir metot varsa, Java ortamı çalıştırma zamanında metodun hangi sınıfa ait tanımdan çalıştırılacağını dinamik olarak belirleyebilir. Bu özelliğe <b>çok biçimlilik(polymorphism)</b> denir.

Aşağıdaki örnekte ```Animal``` ana sınıfına ait ```sound``` metodu çağrılıyor. Hayvan ana sınıfından domuz, kedi, köpek, kuş gibi sınıflar türetilebilir. Onlar hayvan sesini kendi içlerinde farklılaştırabilir ve ```sound``` metoduna farklı görevler yükleyebilir. Böylece nesne yönelimli programlanın çok biçimlilik özelliği, tek bir eylemi farklı şekillerde gerçekleştirmemizi sağlar. 
<br />

```java
package polymorphism;

public class Animal {
  public void sound() {
    System.out.println("The animal makes a sound");
  }
}

public class Pig extends Animal {
  public void sound() {
    System.out.println("The pig says: wee wee");
  }
}

public class Dog extends Animal {
  public void sound() {
    System.out.println("The dog says: bow wow");
  }
}

public class Program {
  public static void main(String[] args) {
    Animal myAnimal = new Animal();  // Create an Animal object
    Animal myPig = new Pig();  // Create a Pig object
    Animal myDog = new Dog();  // Create a Dog object
    myAnimal.sound();
    myPig.sound();
    myDog.sound();
  }
}
```
<br />
### Soyutlama(Abstraction)
Alt sınıfların ortak özelliklerini, işlevlerini taşıyan ancak bir nesne oluşturulamayan üst sınıflara <b>soyut(abstract) sınıflar</b> denir. Soyut sınıf içinde şablon olması açısından metot tanımları yapılabilir veya <b>soyut metotlar</b> yazılabilir. Soyut metoda sahip bir sınıf soyut hale gelir ve <b><u>soyut sınıflardan nesne oluşturulamaz</u></b>.

Java dilinde bir sınıfı soyut olarak tanımlamak için <b>abstract</b> veya <b>interface</b> anahtar sözcükleri kullanılır.


Aşağıda yer alan kod parçasında ```Employee``` tipinde bir soyut sınıf ve bu soyut sınıftan türeyen ```Contractor``` ve ```FullTimeEmployee``` tipinde 2 farklı alt sınıf vardır. 

Her iki tip ```Employee``` nesnesinin de ismi ve saatlik ücret bilgisi olacağından bu özellikler üst sınıfta tanımlanmıştır. Ancak çalışanların saatlik çalışma ücretini hesaplayan metot ```calculateSalary()```, alt sınıfların kendi içinde farklılık göstermektedir. Bu implementasyonun abstract sınıf kullanılarak soyutlanması sağlanmıştır.

```java
package abstraction;

public abstract class Employee {
    
    private String name;
    private int paymentPerHour;
    
    public Employee(String name, int paymentPerHour) {
        this.name = name;
        this.paymentPerHour = paymentPerHour;
    }
    
    public abstract int calculateSalary();

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getPaymentPerHour() {
        return paymentPerHour;
    }

    public void setPaymentPerHour(int paymentPerHour) {
        this.paymentPerHour = paymentPerHour;
    }
}
```

```java
package abstraction;

public class Contractor extends Employee {
    private int workingHours;

    public Contractor(String name, int paymentPerHour, int workingHours) {
        super(name, paymentPerHour);
        this.workingHours = workingHours;
    }

    @Override
    public int calculateSalary() {
        return getPaymentPerHour() * workingHours;
    }
}
```

```java
package abstraction;

public class FullTimeEmployee extends Employee {
    public FullTimeEmployee(String name, int paymentPerHour) {
        super(name, paymentPerHour);
    }
    
    @Override
    public int calculateSalary() {
        return getPaymentPerHour() * 8;
    }
}
```

Bir sonraki makalede görüşmek üzere...