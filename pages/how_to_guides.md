---
layout: page
title: Documentation/How-to guides
permalink: /how_to_guides/
---

# How-to guides

The how-to guides are here to address specific tasks and help you to get things done.

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.how_to_guides  %}        
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>
