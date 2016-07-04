---
position: 5
layout: default
title: Repositories
permalink: repositories.html
published: true
---
The following is all GitHub repositories used in this project

## GitHub rerositories
<ol>
{% for resource in site.data.repositories %}
<li>{{resource.title}} <a href="{{resource.url}}"> {{resource.url}} </a></li>
{% endfor %}
</ol>
