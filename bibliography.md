---
position: 5
layout: default
title: Bibliography
permalink: bibliography.html
published: true
---
The following is a non-exhaustive list of the resources that have been reviewed along

## Books
<ol>
{% for resource in site.data.bibliography.books %}
	<li>{{resource.author}}. {{resource.title}}. {{resource.publisher}}, {{resource.year}}.</li>
{% endfor %}
</ol>

## Online articles and resources

<ol>
{% for resource in site.data.bibliography.blogposts %}
	<li>{{resource.title}} [{{resource.url}}]({{resource.url}})</li>
{% endfor %}
</ol>

## Scholar articles

<ol>
{% for resource in site.data.bibliography.papers %}
	<li>{{resource.authors}}. {{resource.title}}. {{resource.journal}}, {{resource.year}}.</li>
{% endfor %}
</ol>
