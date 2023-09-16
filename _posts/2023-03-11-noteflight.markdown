---
layout: post
title: 'Something I learned about web security'
date: 2023-03-10 13:35:34 -0400
categories: jekyll update
---

In the past, I wrote music using Noteflight. To save time, I wanted to find Noteflight's API to programmatically download all the scores I wrote. Of course, they don't have a public API, but I was thinking that if I tried hard enough, I could find the exact REST API calls they used and call them myself.

Unfortunately, I realized that this was not possible (maybe with web scraping). You see, calling the Noteflight server requires a consumer key and secret and those aren't available to the user unless the user gets them from Noteflight.

The way Noteflight sends requests is with a session cookie. So the consumer key and secret are never exposed in the ajax requests sent to the server.
