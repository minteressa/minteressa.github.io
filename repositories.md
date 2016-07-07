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
{% for resource in site.data.repositories.repository %}
<li>{{resource.title}} <a href="{{resource.url}}">{{resource.url}}</a></li>
{% endfor %}
</ol>

<ol>
{% for resource in site.data.repositories.repository %}
<li><div id="{{resource.user}}_{{resource.title}}"></div></li>
{% endfor %}
</ol>

<script>
$("#{{resource.user}}_{{resource.title}}").hubInfo({ 
  user: "{{resource.user}}",
  repo: "{{resource.title}}"
});
</script>