---
layout: default
title: "posts"
sidebar_link: true
---

<h3> posts </h3>
<div class="posts">
  {% for post in site.posts %}
    <div>
       <span> {{ post.date | date_to_string }} ~ </span> <a href="{{ post.url }}">{{ post.title }}</a> 
    </div>
  {% endfor %}
</div>