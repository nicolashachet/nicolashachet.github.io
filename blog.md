---
layout: post
title: Blog
---

Retrouvez les archives de mon blog personnel créé en 2011 (https://blog.nicolashachet.com) cumulant 3 millions de visiteurs uniques pour 4,5 millions de pages vues au total. 

{% for post in site.posts %}
<div class="mb-2">
    {% include svg/nav-arrow-right.svg %}
    <a href="{{ post.url }}"><small class="text-secondary">[{{ post.date | date: "%Y" }}][{{ post.categories }}]</small> {{ post.title }}</a>
</div>
{% endfor %}
