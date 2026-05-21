---
title: Blog
layout: posts
permalink: /posts/
entries_layout: list
paginate: true
---
# My Blog Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span>({{ post.date | date_to_string }})</span>
    </li>
  {% endfor %}
</ul>

