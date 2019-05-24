---
layout: default
title: Life Story
slug: Life Story, Love and Glory.
permalink: /lifestory/
category: home
---

{% for story in site.categories.lifestory %}
<h2><a href="{{ story.url }}">{{ story.title }}</a></h2>
<p>{{ story.slug }}</p>
{% endfor %}
