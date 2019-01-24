---
layout: default
permalink: /my-back-pages
title: My Back Pages
slug: I was so much older than, I'm younger than that now.
---

<ul>
    {% for post in site.posts %}
  <li>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p>{{ category.slug | markdownify }}</p>
  </li>
  {% endfor %}
</ul>
