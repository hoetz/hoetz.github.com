---
layout: page
title: Welcome to Florian Hötzinger's Blog
tagline: complications in .NET
---
{% include JB/setup %}

##Welcome to Florian Hötzinger's Blog

Here's a sample "posts list".

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>




