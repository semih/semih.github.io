---
layout: post
title: "String İfadeyi Tersine Çevirme"
date: 2017-09-12 18:31ly
author: semih
comments: true
lang: tr
lang-ref: string
categories: [Algorithm, Java]
tags: [java, algorithm]
published: false
---
Bu örnekte string ifadeyi nasıl tersine çevirebileceğimizi inceleyeceğiz.
{% highlight java %}
public class ReverseString {

	public static void main(String[] args) {
		String s = "Hello world!";
		System.out.println("Reversed String: " + reverse(s));
	}

	public static String reverse(String str) {
        StringBuilder strBuilder = new StringBuilder();
        char[] strChars = str.toCharArray();

        for (int i = strChars.length - 1; i >= 0; i--) {
            strBuilder.append(strChars[i]);
        }

        return strBuilder.toString();
    }
}
{% endhighlight %}

Çıktı:
{% highlight java %}
String ifadenin ters çevrilmiş hali: !dlrow olleH
{% endhighlight %}
