---
layout: archive
permalink: /ML_AI/
title: "ML & AI"
author_profile: true
header:
---

{% include adsense.html %}
{% include group-by-array collection=site.posts field="tags" %}

{% for tag in group_names %}
    {% if tag == "<ML&AI" %}
	  {% assign posts = group_items[forloop.index0] %}
<!---	  <h2 id="{{ tag | slugify }}" class="archive__subtitle">{{ tag }}</h2> -->
	  {% for post in posts %}
	    {% include archive-single.html %}
	  {% endfor %}
	 {% endif %}
{% endfor %}
