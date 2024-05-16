---
layout: post
title: Blog
---

Retrouvez les articles de mon blog personnel : https://blog.nicolashachet.com.
La plupart sont des articles archives rédigés sur des sujets techniques, les plus récents sont des posts linkedin. 

{% for post in site.posts %}
<div class="mb-2">
    {% include svg/nav-arrow-right.svg %}
    <a href="{{ post.url }}"><small class="text-secondary">[{{ post.date | date: "%Y" }}][{{ post.categories }}]</small> {{ post.title }}</a>
</div>
{% endfor %}
