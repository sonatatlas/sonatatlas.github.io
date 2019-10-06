---
layout: default
title: My Back Pages
permalink: /backpages/
slug: I was so much older than, I'm younger than that now.
categories: [ home ]
---

{% for post in site.categories.backpages %}
<h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
{% endfor %}
