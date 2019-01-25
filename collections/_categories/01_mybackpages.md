---
layout: default
permalink: /my-back-pages
title: My Back Pages
slug: I was so much older than, I'm younger than that now.
---

<ul>
    {% for backpage in site.backpages %}
  <li>
    <h2><a href="{{ backpage.url }}">{{ backpage.title }}</a></h2>
  </li>
  {% endfor %}
</ul>
