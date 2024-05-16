---
layout: post
title: Blog
---

Retrouvez les articles issues du blog https://blog.nicolashachet.com.
La plupart sont des archives d'articles rédigés sur des sujets techniques, certains sont des posts linkedin plus récents 

{% for post in site.posts %}
<div class="mb-2">
    {% include svg/nav-arrow-right.svg %}
    <a href="{{ post.url }}"><small class="text-secondary">[{{ post.date | date: "%Y" }}][{{ post.categories }}]</small> {{ post.title }}</a>
</div>
{% endfor %}
