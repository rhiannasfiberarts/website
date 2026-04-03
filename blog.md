---
layout: default
title: Blog
permalink: /blog/
---

<div class="blog-page container">
  <header class="page-header">
    <h1>Blog</h1>
  </header>

  <div class="post-list">
    {% for post in site.posts %}
    <article class="post-card">
      {% if post.cover_image %}
      <a href="{{ post.url | relative_url }}" class="post-card-image">
        <img src="{{ post.cover_image | relative_url }}" alt="{{ post.title }}">
      </a>
      {% endif %}
      <div class="post-card-body">
        <time class="post-date">{{ post.date | date: "%B %-d, %Y" }}</time>
        {% if post.tags and post.tags.size > 0 %}
        <span class="post-tags">
          {% for tag in post.tags %}<span class="tag">{{ tag }}</span>{% endfor %}
        </span>
        {% endif %}
        <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
        <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 40 }}</p>
        <a href="{{ post.url | relative_url }}" class="read-more">Read more &rarr;</a>
      </div>
    </article>
    {% endfor %}

    {% if site.posts.size == 0 %}
    <p class="empty-state">No posts yet — check back soon!</p>
    {% endif %}
  </div>
</div>
