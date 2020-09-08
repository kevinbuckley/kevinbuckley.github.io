---
layout: default
title: "posts"
sidebar_link: true
---

<div class="posts">
  {% for post in site.posts %}
    <div class="dt">{{ post.date | date_to_string }} </div>
    <div><a href="{{ post.url }}">{{ post.title }}</a> </div>
    {{ post.excerpt }}

  {% endfor %}
</div>