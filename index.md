---
layout: index
title: "posts"
---

<h1> Posts </h1>
<div class="posts">
  {% for post in site.posts %}
    <div>
      <a href="{{ post.url }}">{{ post.title }}</a> <i>- posted on  {{ post.date | date_to_string }}</i>
      {{ post.excerpt }}
    </div>
  {% endfor %}
</div>