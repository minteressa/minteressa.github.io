---
position: 4
layout: default
title: Blog
permalink: blog/
---
{% for post in site.posts %}
<div class="row">
  <div class="col-xs-12">
    <img class="img-responsive" src="{{ post.thubmnail }}" alt="{{ post.title }}"/>
    <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
    <h2>
      <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
    </h2>
    <p>{{post.excerpt}}<a href="{{post.url}}">Read more...</a></p>
  </div>
</div>
{% endfor %}