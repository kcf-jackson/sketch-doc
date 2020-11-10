---
layout: page
title: 'Documentation/Reference'
permalink: /reference/
---

# Reference

The reference section contains information about the package functions (R and JavaScript) and also some other resources.

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.reference  %}        
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>

