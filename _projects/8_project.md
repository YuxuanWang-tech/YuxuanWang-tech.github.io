---
layout: page
title: Beyond the Code
description: Structure in Physics, Emotion in Music.
img: assets/img/9.jpg # 建议放一张你弹琴、跳舞或在舞台上的高质感照片
importance: 3
category: Extracurricular # 这个分类会自动在 Projects 页面单开一个版块
giscus_comments: true
---

While my academic life is driven by rigorous mathematical structures and high-performance computing, my personal life is deeply rooted in artistic expression and community building. I firmly believe that the creativity required to compose a melody or choreograph a performance is the exact same creativity needed to solve a complex non-linear physics problem.

**"Structure in Physics, Emotion in Music."** This philosophy shapes my approach to both science and life.

---

### 🎭 Stage & Art Direction
During my time at Xi'an Jiao Tong University, I was deeply involved in the performing arts.
* **Art Director & Deputy Leader:** I served as the Art Director and Deputy Leader of the Student Art Troupe. In this role, I managed and coordinated large-scale, university-level activities, including orientation and graduation ceremonies.
* **Fitness Dance Association:** Driven by a passion for movement and team coordination, I served as Minister of the Fitness Dance Association (ADA). I actively collaborated with the University Athletic Department to establish this new club, organizing classes and competitions to enrich student life.

These experiences taught me how to lead diverse teams, make high-pressure decisions, and translate a creative vision into a flawlessly executed event.

---

### 🌍 Cross-Cultural Leadership
My engineering studies in France (Ecole Centrale de Lille) offered a unique opportunity to build bridges between different cultures.
* **Secretary of the Chinese Culture Club:** I took on the role of Secretary, where I actively promoted Chinese culture to French students through lectures and evening events.
* **Community Integration:** I focused on fostering communication and helping international students seamlessly integrate into the broader academic collective. 

Working across linguistic and cultural boundaries has profoundly shaped my communication skills, a trait I consider essential for collaborating in global, fast-paced environments.

---

### 🎵 Musical & Creative Showcase
*(Note: I compose and arrange music in my free time. Here are some of my creative projects.)*

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        <iframe width="100%" height="315" src="https://www.youtube.com/embed/YOUR_VIDEO_ID" title="Music Performance" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    </div>
</div>

> "Whether debugging a Python pipeline or harmonizing a chord progression, it's all about finding the underlying pattern."


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, _bled_ for your project, and then... you reveal its glory in the next row of images.

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
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
    {% include figure.liquid path="assets/img/6.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/11.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
```

{% endraw %}
