---
position: 5
layout: default
title: Repositories
permalink: repositories.html
published: true
---
The following is a list of all GitHub repositories used in this project

## GitHub repositories
<ol>
{% for resource in site.data.repositories %}
<li>{{repository.title}} <a href="{{repository.url}}"> {{repository.url}}</a></li>
{% endfor %}
</ol>
