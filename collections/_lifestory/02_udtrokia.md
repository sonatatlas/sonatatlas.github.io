---
layout: default
title: udtrokia
slug: Aug 23, 2016 - Nov 18, 2017
---

{%- for post in site.posts -%}
{%- if post.category == "udtrokia" -%}
<h2><a href="{{post.url}}">{{ post.title }}</a></h2>
<p>{{ post.date | date: site.format }}</p>
{%- endif -%}
{%- endfor -%}
