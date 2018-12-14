---
layout: archive
permalink: /enespanol/
title: "En Español"
---

{{ content }}

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

{% for post in paginator.posts %}
  {% include archive-single.html %}
{% endfor %}

{% include paginator.html %}

<style>
img {
    display: block;
    margin-left: auto;
    margin-right: auto;
}
</style>

