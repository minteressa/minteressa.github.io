---
position: 7
layout: default
title: Bibliography
permalink: bibliography.html
published: true
---
The following is a non-exhaustive list of the resources that have been reviewed along

## Books

<ol>
{% for resource in site.data.bibliography.books %}
	<li>{{resource.author}}. <i>{{resource.title}}</i>. {{resource.publisher}}, {{resource.year}}.</li>
{% endfor %}
</ol>

## Online articles and resources

<ol>
{% for resource in site.data.bibliography.blogposts %}
<li><a href="{{resource.url}}"> {{resource.title}} </a></li>
{% endfor %}
</ol>

## Scholarly articles

<ol>
{% for resource in site.data.bibliography.papers %}
<li>{{resource.authors}}. <i>{{resource.title}}</i>. {{resource.journal}}, {{resource.year}}.</li>
{% endfor %}
</ol>
