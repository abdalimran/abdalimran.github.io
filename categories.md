---
layout: page
title: Posts by Category
permalink: /categories/
---

<div id="archives">
{% for category in site.categories %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first}}{% endcapture %}
    <h3 class="category-head">{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
	    <article class="archive-item">
	      &nbsp; &nbsp; &nbsp; &nbsp;<span>{{ post.date | date_to_string }}</span> &nbsp; <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
	    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>