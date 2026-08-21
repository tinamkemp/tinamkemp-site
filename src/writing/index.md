---
layout: base.njk
title: Writing
---

<h1>Writing</h1>

<p>Under construction</p>

<ul class="post-list">
{% for post in collections.posts %}
  <li>
    <a href="{{ post.url }}">{{ post.data.title }}</a>
    <span class="post-date">{{ post.data.date | readableDate }}</span>
    <p>{{ post.data.excerpt }}</p>
  </li>
{% endfor %}
</ul>
