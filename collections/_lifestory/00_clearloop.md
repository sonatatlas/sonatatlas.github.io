---
layout: default
title: clearloop
slug: Nov 18, 2018 -
---

{%- for post in site.posts -%}
{%- if post.category == "clearloop" -%}
<h2><a href="{{post.url}}">{{ post.title }}</a></h2>
<p>{{ post.date | date: site.format }}</p>
{%- endif -%}
{%- endfor -%}
