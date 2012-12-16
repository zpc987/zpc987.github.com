---
layout: page
title: 橙子的博客
tagline:
---
{% include JB/setup %}

　　<p>最新文章</p>
　　<ul>
　　　　{% for post in site.posts %}
　　　　　　<li>{{ post.date | date_to_string }} <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
　　　　{% endfor %}
　　</ul>
