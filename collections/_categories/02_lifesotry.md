---
layout: default
permalink: /life-story
title: Life Story
slug: Life Story, Love and Glory.
---

{% for story in site.lifestory %}
<h2><a href="{{ story.url }}">{{ story.title }}</a></h2>
<p>{{ story.slug }}</p>
{% endfor %}
