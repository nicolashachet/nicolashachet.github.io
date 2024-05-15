---
layout: post
title: Blog
---

{% for post in site.posts %}
<div class="mb-2">
    {% include svg/nav-arrow-right.svg %}
    <a href="{{ post.url }}"><small class="text-secondary">[{{ post.date | date: "%Y" }}][{{ post.categories }}]</small> {{ post.title }}</a>
</div>
{% endfor %}
