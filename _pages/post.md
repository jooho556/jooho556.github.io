---
layout: page
title: Posts
---

<div class="posts">
  {% for projects in paginator.posts %}
  <div class="post">
    <h1 class="post-title">
      <a href="{{post.url}}">
        {{ post.title }}
      </a>
    </h1>
    {{  post.excerpt }}
  </div>
  {% endfor %}
</div>
