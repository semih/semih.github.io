---
layout: post
title: "Binary Search"
date: 2017-09-16 01:15ly
author: semih
comments: true
lang: en
lang-ref: binary-search
categories: [algorithm]
tags: [java, algorithm]
published: true
---
In the following example, you will see the recursive binary search algorithm implementation in Java language.
{% highlight java %}
class BinarySearch {

	public static void main(String args[]) {
		BinarySearch binarySearchObject = new BinarySearch();
		int array[] = { 1, 8, 26, 45, 93 };
		int arrayLength = array.length;
		int x = 45;
		int result = binarySearchObject.binarySearch(array, 0, arrayLength - 1, x);
		if (result == -1) {
			System.out.println("Element not present");
		}
		else {
			System.out.println("Element found at index " + result);
		}
	}
	
	// Returns index of x if it is present in arr[l..r], else return -1
	int binarySearch(int arr[], int l, int r, int x) {
		if (r >= l) {
			int mid = l + (r - l) / 2;

			// If the element is present at the
			// middle itself
			if (arr[mid] == x)
				return mid;

			// If element is smaller than mid, then
			// it can only be present in left subarray
			if (arr[mid] > x)
				return binarySearch(arr, l, mid - 1, x);

			// Else the element can only be present
			// in right subarray
			return binarySearch(arr, mid + 1, r, x);
		}

		return -1;
	}
}
{% endhighlight %}

Output:
{% highlight java %}
Element found at index 3
{% endhighlight %}
