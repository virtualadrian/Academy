---
date: 2017-02-07
title: Reading time
video_id: hOvVjZh9-rs
description: A simple way to calculate the read time of a post
tags:
  - jekyll-liquid
resources:
  - name: Source code
    link: https://github.com/CloudCannon/bakery-store/tree/reading-time
  - name: Reading Time without plugins
    link: http://carlosbecker.com/posts/jekyll-reading-time-without-plugins
type: Video
set: advanced
set_order: 4
---
## Introduction

[Medium](https://medium.com) has a nice little feature that shows an estimated reading time on posts. 

![Medium Michael Rose](/images/tutorials/reading-time/medium.jpg){: .screenshot}

So how would we accomplish this with Jekyll? [Carlos Becker](http://carlosbecker.com/posts/jekyll-reading-time-without-plugins) came up with a simple Liquid script which can calculate this for us.

## The algorithm

First we need to calculate how many word are on the page using the `number_of_words` filter. Then we can divide the number of words by 180 ([the average number of words per minute a human reads at](https://en.wikipedia.org/wiki/Words_per_minute)) and we have an estimated read time.

We also need to handle the case where the estimated read time is less than 2 minutes (360 words). In this case we'll show "1 min".

{% raw %}
~~~liquid
{% assign words = content | number_of_words %}
{% if words < 360 %}
  1 min
{% else %}
  {{ words | divided_by:180 }} mins
{% endif %}
~~~
{% endraw %}

![Finished read time](/images/tutorials/reading-time/finished.png){: .screenshot}
