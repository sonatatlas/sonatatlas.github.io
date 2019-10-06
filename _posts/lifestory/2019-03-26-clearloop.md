---
layout: default
title: clearloop
slug: Nov 18, 2018 -
category: lifestory
---

{%- for post in site.categories.clearloop -%}
<h2><a href="{{ post.url}}">{{ post.title }}</a></h2>
<p>{{ post.date | date: site.format }}</p>
{%- endfor -%}
