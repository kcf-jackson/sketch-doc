---
layout: page
title: Documentation/Explanation
permalink: /explanation/
---

# Explanation

The explanation section covers conceptual topics and helps you understand the package better. 
You may find this section useful if you are debugging your sketch application or building a large-scale application.

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.explanation  %}        
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>
