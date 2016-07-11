---
position: 6
layout: default
title: Visualization
permalink: visualization.html
---
The following is a non-exhaustive list of the resources that have been reviewed along

## Books
<ol>
{% for resource in site.data.bibliography.books %}
	<li>{{resource.title}}</li>
{% endfor %}
</ol>

## Online articles and resources

<ol>
{% for resource in site.data.bibliography.blogposts %}
	<li>{{resource.title}}</li>
{% endfor %}
</ol>

## Scholar articles

<ol>
{% for resource in site.data.bibliography.papers %}
	<li>{{resource.title}}</li>
{% endfor %}
</ol>