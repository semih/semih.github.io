---
layout: post
title: "Fibonacci"
date: 2017-09-14 01:15ly
author: semih
comments: true
lang: en
lang-ref: fibonacci
categories: [Algorithm]
tags: [java, algorithm]
published: true
---
In the following example, fibonacci numbers are written for given input in Java language.
{% highlight java %}
public class Fibonacci {

	public static void main(String[] args) {
		int n = 9;
		fib(n);
	}

	static int fib(int n) {
		/* Declare an array to store Fibonacci numbers. */
		int f[] = new int[n + 2]; // 1 extra to handle case, n = 0
		int i;

		/* 0th and 1st number of the series are 0 and 1 */
		f[0] = 0;
		f[1] = 1;

		for (i = 2; i <= n; i++) {
			/*
			 * Add the previous 2 numbers in the series and store it
			 */
			f[i] = f[i - 1] + f[i - 2];
			System.out.print(f[i] + " ");
		}

		return f[n];
	}
}
{% endhighlight %}

Output:
{% highlight java %}
1 2 3 5 8 13 21 34 
{% endhighlight %}
