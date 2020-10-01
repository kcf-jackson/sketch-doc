---
layout: page
title: Tutorials
permalink: /tutorials/
---

# Tutorials [Work In Progress] / Gallery

The tutorials are work in progress. In the meantime, here are some visualisations made in R using our package!

<style> 
.gallery-item {
    display: flex;
    flex-flow: wrap;
}
</style>
<div class="container">
    <hr>
    <h3> Simulation </h3>
    <div style="display:grid; grid-template-columns: 0.834fr 1.16fr 1fr;">
        <div>
            <div>Particles system - p5.js</div>
            <img src="gallery/epi.gif" alt="">
        </div>
        <div>
            <div>Game of life - p5.js</div>
            <img src="gallery/game_of_life.gif" alt="">
        </div>
        <div>
            <div>Leaflet.js and AgentMaps.js</div>
            <img src="gallery/agent_maps.gif" alt="">
        </div>
    </div>
    <hr>
    <h3>Physics engines and 3D models</h3>
    <div style="display:grid; grid-template-columns: 0.552fr 1fr;">
        <div>
            <div>matter.js</div>
            <img src="gallery/galton_board.gif" alt="">
        </div>
        <div>
            <div>three.js</div>
            <img src="gallery/three_js.gif" alt="">
        </div>
    </div>
    <hr>
    <h3> Plotting / Charting libraries</h3>
    <div style="display:grid; grid-template-columns: 0.585fr 1fr;">
        <div>
            <div>plotly.js</div>
            <img src="gallery/plotly.gif" alt="">
        </div>
        <div>
            <div>chart.js</div>
            <img src="gallery/chart_js.gif" alt="">
        </div>
    </div>
    <hr>
    <h3> Creative coding </h3>
    <div style="display:grid; grid-template-columns: 0.6fr 1fr;">
        <div>
            <div> p5.js </div>
            <img src="gallery/creative_coding.png" alt="">
        </div>
        <div>
            <div>Circles packing - p5.js</div>
            <img src="gallery/circle_packing.gif" alt="">
        </div>
    </div>
    <h3> Publishing </h3>
    <div style="display:grid; grid-template-columns: 1fr 1fr 1fr;">
        <div>
            <div>p5.js - replicated from <a href="https://interaktiv.morgenpost.de/berlin-marathon-2016/">this</a></div>
            <img src="gallery/marathon.gif" alt="">
        </div>
        <div>
            <div>d3.js - replicated from <a href="https://www.themarshallproject.org/2015/08/04/the-new-science-of-sentencing">this</a>, data are simulated</div>
            <img src="gallery/interactive_table.gif" alt="">
        </div>
        <div>
            <div>d3.js - replicated from <a href="https://archive.nytimes.com/www.nytimes.com/interactive/2013/05/07/education/college-admissions-gap.html">this</a>, data are simulated</div>
            <img src="gallery/d3_js.gif" alt="">
        </div>
    </div>
</div>

<div class="section-index">
    <hr class="panel-line">
    {% for post in site.tutorials  %}        
    <div class="entry">
    <h5><a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a></h5>
    <p>{{ post.description }}</p>
    </div>{% endfor %}
</div>

