---
position: 5
layout: default
title: Repositories
permalink: repositories.html
published: true
---
The following is all GitHub repositories used in this project

## GitHub repositories
<ol>
{% for resource in site.data.repositories %}
<li>{{repositories.title}} <a href="{{repositories.url}}"> {{repositories.url}} </a></li>
{% endfor %}
</ol>
