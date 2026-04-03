---
layout: default
title: Gallery
permalink: /gallery/
---

<div class="gallery-page container">
  <header class="page-header">
    <h1>Gallery</h1>
    <p class="page-description">A visual archive of finished pieces, works in progress, and materials I love.</p>
  </header>

  <!-- ============================================================
       STANDALONE GALLERY IMAGES
       Add extra photos here that aren't tied to a specific post.
       Format:
         - image: assets/images/your-photo.jpg
           caption: "Optional caption"     ← optional
           link:                           ← leave blank for no link
       ============================================================ -->
  {% assign standalone = page.extra_images %}

  <!-- Collect all images from blog posts -->
  {% assign post_images = "" | split: "" %}
  {% for post in site.posts %}
    {% if post.cover_image %}
      {% assign item = post | inspect %}
      {% assign post_images = post_images | push: post %}
    {% endif %}
    {% if post.images %}
      {% for img in post.images %}
        {% assign post_images = post_images | push: post %}
      {% endfor %}
    {% endif %}
  {% endfor %}

  <div class="gallery-grid gallery-grid--large">

    <!-- Post-linked images first -->
    {% for post in site.posts %}
      {% assign all_post_images = "" | split: "" %}
      {% if post.cover_image %}
        {% assign all_post_images = all_post_images | push: post.cover_image %}
      {% endif %}
      {% if post.images %}
        {% for img in post.images %}
          {% assign all_post_images = all_post_images | push: img %}
        {% endfor %}
      {% endif %}

      {% for img_src in all_post_images %}
      <div class="gallery-item gallery-item--linked">
        <a href="{{ post.url | relative_url }}" title="{{ post.title }}">
          <img src="{{ img_src | relative_url }}" alt="{{ post.title }}">
          <div class="gallery-overlay">
            <span class="gallery-overlay-text">{{ post.title }}</span>
          </div>
        </a>
      </div>
      {% endfor %}
    {% endfor %}

    <!-- Standalone extra images (defined in this page's front matter) -->
    {% if page.extra_images %}
      {% for item in page.extra_images %}
      <div class="gallery-item">
        {% if item.link %}
        <a href="{{ item.link }}" {% if item.link contains 'http' %}target="_blank" rel="noopener"{% endif %}>
          <img src="{{ item.image | relative_url }}" alt="{{ item.caption | default: 'Gallery photo' }}">
          {% if item.caption %}
          <div class="gallery-overlay"><span class="gallery-overlay-text">{{ item.caption }}</span></div>
          {% endif %}
        </a>
        {% else %}
        <img src="{{ item.image | relative_url }}" alt="{{ item.caption | default: 'Gallery photo' }}">
        {% if item.caption %}<p class="gallery-caption">{{ item.caption }}</p>{% endif %}
        {% endif %}
      </div>
      {% endfor %}
    {% endif %}

  </div>
</div>
