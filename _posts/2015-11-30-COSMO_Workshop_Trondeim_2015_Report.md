---
layout: post
title: Pictures from workshop in Trondheim, 2015
---
As guests in FIX Makerspace we were giving a COSMO Workshop in Trondheim from 29.-30. November 2015. Here are some pictures from the workshop

{% for image in site.static_files %}
{% if image.path contains 'images/WorkshopTrondheim2015' %}
<img src="{{ site.baseurl }}{{ image.path }}" alt="image" />
{% endif %}
{% endfor %}
