---
layout: archive
title: Archive
permalink: /archive/
---

<div id="archives">
{% assign sortedcats = site.categories | sort %}
{% for category in sortedcats %}
  <div class="archive-group">
    {% capture category_name %}{{ category | first}}{% endcapture %}
    <h3 class="category-head">{{ category_name }}</h3>
    <!-- <h3 class="category-head"></h3> -->

    <a name="{{ category_name | slugize }}"></a>
    {% for post in site.categories[category_name] %}
	    <article class="archive-item">
	      &nbsp; &nbsp; &nbsp; &nbsp;<span>{{ post.date | date_to_string }}</span> &nbsp; <a target="_blank" href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
	    </article>
    {% endfor %}
  </div>
{% endfor %}
</div>