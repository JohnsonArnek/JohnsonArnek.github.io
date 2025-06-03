---
layout: page # Or a custom layout if you make one
title: All Writings
permalink: /blog/ # Or /archive/
---

<h1>{{ page.title }}</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a> - {{ post.date | date: "%B %d, %Y" }}
      {% if post.categories.size > 0 %}
        <br/>Categories: {{ post.categories | join: ", " }}
      {% endif %}
    </li>
  {% endfor %}
</ul>
