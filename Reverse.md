---
title: reverse
layout: home
permalink: /reverse/
---

# Reverse Engineering Blog

Here are all the posts related to reverse engineering:

<ul>
  {% for post in site.posts %}
    {% if post.category == "reverse" %}
      <li>
        {%- assign date_format = "%Y-%m-%d" -%}
        [{{ post.date | date: date_format }}] -> <a href="{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endif %}
  {% endfor %}
</ul>
