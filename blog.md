---
layout: page
title: Blog
permalink: /blog/
---

{% for post in site.posts %}
<h4><a href="{{ post.url }}">{{ post.title }}</a></h4>
  <p>{{ post.date | date_to_string }}</p>
{% endfor %}
