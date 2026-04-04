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
    {% assign shown_paths = "" | split: "" %}

    {% comment %}Post-linked images, newest post first{% endcomment %}
    {% for post in site.posts %}
      {% assign post_imgs = "" | split: "" %}
      {% if post.cover_image %}
        {% assign post_imgs = post_imgs | push: post.cover_image %}
      {% endif %}
      {% if post.images %}
        {% for img in post.images %}
          {% assign post_imgs = post_imgs | push: img %}
        {% endfor %}
      {% endif %}

      {% for img_src in post_imgs %}
        {% assign img_path = img_src | prepend: "/" %}
        {% unless shown_paths contains img_path %}
          {% assign shown_paths = shown_paths | push: img_path %}
          <div class="gallery-item gallery-item--linked">
            <a href="{{ post.url | relative_url }}" title="{{ post.title }}">
              <img src="{{ img_src | relative_url }}" alt="{{ post.title }}">
              <div class="gallery-overlay">
                <span class="gallery-overlay-text">{{ post.title }}</span>
              </div>
            </a>
          </div>
        {% endunless %}
      {% endfor %}
    {% endfor %}

    {% comment %}Standalone images not associated with any post{% endcomment %}
    {% for image in all_images %}
      {% unless shown_paths contains image.path %}
        <div class="gallery-item">
          <img src="{{ image.path | relative_url }}" alt="Gallery photo">
        </div>
      {% endunless %}
    {% endfor %}

  </div>
</div>
