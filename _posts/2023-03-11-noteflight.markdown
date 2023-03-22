---
layout: post
title: "Could not use Noteflight API to download all my past scores"
date: 2023-03-10 13:35:34 -0400
categories: jekyll update
---

Unfortunately, I cannot use Noteflight's API to download all my scores. The Noteflight API requires a consumer key and secret and those aren't available to the user unless the user gets them from Noteflight. 

The way Noteflight sends requests is with a session cookie. So the consumer key and secret are never exposed in the ajax requests sent to the server. Very unfortunate. 