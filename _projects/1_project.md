---
layout: page
title: Database Sructure 
description: Case Study With Entity-Relationship Diagram
img: assets/img/erd_pharmacy.png
importance: 1
category: work
related_publications: 
---

## Synopsis 
Database design for a ‘Connected Health’ business strategy at an extensive pharmacy network.
 
## Situation  
Recent changes in provincial regulations in Canada enable pharmacists to provide a growing list of medical services including: vaccinations, medical reviews, and treatments for minor ailments, in addition to their traditional role as prescription dispensers. Importantly, primary pharmacy IT systems deployed in the network are decentralized (each pharmacy is an independent unit) and transactional (capturing transactions at the pharmacy and not designed for patient treatments). How may the network pivot rich historical data captured in thousands of pharmacies into a central and patient-centric system that will better support the emerging roles of pharmacists as healthcare providers? How can we support patients receiving treatment in multiple pharmacies? How can we measure the health outcomes of patients and make proper recommendations for products and services? 



</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/pharmacy_erd.png" title="database erd" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Schematic Entity-Relationship Diagram (ERD) of pharmacy data.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal its glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

{% raw %}
```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```
{% endraw %}
