---
layout: default
title: Content per category
---
{% capture categories %}
  {% for category in site.categories %}
    {{ category[0] | downcase }}
  {% endfor %}
{% endcapture %}
{% assign sortedcategories = categories | split:' ' | uniq | sort %}

<ul class="inline_list">
  {% assign categories_list = sortedcategories %}
  {% include categories_list.html %}
  {% assign categories_list = nil %}
</ul>
  
{% for category in sortedcategories %} 
  <h2 id="{{ category }}-ref">{{ category | join: "/" }}</h2>
  <ul>
    {% assign pages_list = site.categories[category] %}  
    {% include pages_list.html %}
    {% assign pages_list = nil %}
  </ul>
{% endfor %}