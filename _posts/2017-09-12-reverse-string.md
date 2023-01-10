---
layout: post
title: "Reverse String"
date: 2017-09-12 18:31ly
author: semih
comments: true
lang: en
lang-ref: string
categories: [Algorithm]
tags: [java, algorithm]
published: true
---
In the following example, reversal string operation is shown in Java language. *reverse(s)* method completely reverses the string.
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

Output:
{% highlight java %}
Reversed String: !dlrow olleH
{% endhighlight %}
