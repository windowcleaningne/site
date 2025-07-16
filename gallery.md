
title: Gallery
layout: page
permalink: /gallery
callouts: banner_callouts
hero_height: is-small
hero_image: assets/logo.png
---

# Gallery

Here is a selection of our work...
DETACHED---

<ul class="gallery">
  {% for image in site.static_files %}
    {% if image.path contains 'gallery' %}
      <li class="gallery"><a href="{{ image.path }}" target="_blank"><img src="{{ image.path }}" /></a></li>
    {% endif %}
  {% endfor %}
</ul>
