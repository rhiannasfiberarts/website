---
layout: default
title: Gallery
permalink: /gallery/
---

<div class="gallery-page container">
  <header class="page-header">
    <h1>Gallery</h1>
  </header>

  <div class="gallery-grid gallery-grid--large">
    {% assign all_images = site.static_files | where_exp: "file", "file.path contains '/assets/images/'" %}

    {% for image in all_images %}
      {% assign linked_post = nil %}

      {% for post in site.posts %}
        {% if post.cover_image %}
          {% assign cover_path = post.cover_image | prepend: "/" %}
          {% if cover_path == image.path %}
            {% assign linked_post = post %}
          {% endif %}
        {% endif %}
        {% if post.images %}
          {% for img in post.images %}
            {% assign img_path = img | prepend: "/" %}
            {% if img_path == image.path %}
              {% assign linked_post = post %}
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}

      <div class="gallery-item {% if linked_post %}gallery-item--linked{% endif %}">
        {% if linked_post %}
          <a href="{{ linked_post.url | relative_url }}" title="{{ linked_post.title }}">
            <img src="{{ image.path | relative_url }}" alt="{{ linked_post.title }}">
            <div class="gallery-overlay">
              <span class="gallery-overlay-text">{{ linked_post.title }}</span>
            </div>
          </a>
        {% else %}
          <img src="{{ image.path | relative_url }}" alt="Gallery photo">
        {% endif %}
      </div>

    {% endfor %}
  </div>
</div>
