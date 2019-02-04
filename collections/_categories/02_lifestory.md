---
layout: default
permalink: /lifestory
title: Lifestory
slug: life story, love and glory.
---

# udtrokia
<ul>
{%- for post in site.posts -%}
<h2>{{ post.title }}</h2>
<strong>{{post.date}}</strong>
<div>{{post.content}}</div>
{%- endfor -%}
</ul>
