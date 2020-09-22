---
layout: page
title: Documentation
permalink: /concepts/
---

# Concepts

This is the index page for the fundamentals of the sketch package.

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.concepts  %}        
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>
