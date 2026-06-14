---
layout: page
title: Blog
permalink: /blog/
---

I occasionally write about research, methodology, tools, and other academic interests.

<div class="post-list">
  {%- for post in site.posts -%}
  <article class="post-preview">
    <h3 class="post-title">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </h3>
    <p class="post-meta">
      {{ post.date | date: "%B %-d, %Y" }}
    </p>
    <p class="post-excerpt">
      {{ post.excerpt | strip_html | truncate: 200 }}
    </p>
    <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
  </article>
  {%- endfor -%}
</div>
