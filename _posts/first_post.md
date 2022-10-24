---
layout: post
title: 'First Blog Post -- One Leetcode'
date: 2022-10-24 15:22:34 -0400
categories: jekyll update
---

Welcome to my first blog post. In this post, I'm just going to solve one Medium level leetcode. Here is the [link](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/) to the problem.

I always code in Python, at least for right now. So that's what I'm going to use here. And it's weird because the index method exists in Python that finds the index of the first substring. So what happens if I just use it?

{% highlight python %}
class Solution(object):
def strStr(self, haystack, needle):
"""
:type haystack: str
:type needle: str
:rtype: int
"""
try:
return haystack.index(needle)
except:
return -1

{% endhighlight %}

It just works. Ok good.
