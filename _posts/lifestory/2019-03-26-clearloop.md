---
layout: default
title: clearloop
slug: Nov 18, 2018 -
category: lifestory
---

{%- for post in site.categories.clearloop -%}
<h1>{{ post.title }}</h1>
<p>{{ post.date | date: site.format }}</p>
{{ post.content }}
<hr style="margin-top: 5vw;">
{%- endfor -%}
