---
layout: default
title: Life story
slug: Life story, love and glory.
---

{% for story in site.lifestory %}
<h2><a href="{{ story.url }}">{{ story.title }}</a></h2>
<p>{{ story.slug }}</p>
{% endfor %}
