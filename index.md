---
layout: home
title: Welcome to my website
---

I'm Ajey, a lead data scientist and an AI researcher with expertise in production ML, multimodal AI systems and deep learning. I currently work at Philo, a streaming platform startup that takes on Youtube TV as a competitor. Concurrently, I collaborate with with the [SPOG Lab](https://spoglab.stanford.edu/) at Stanford as an independent AI researcher, where I'm developing multimodal AI systems that integrate fine-tuned language models with speech processing to study language acquisition in children with cochlear implants.

Durind my PhD in Aerospace Engineering from Purdue, I worked on hierarchical multiscale modeling frameworks. After that, I worked as a postdoctoral researcher at Argonne National Laboratory developing Bayesian deep learning models for nuclear safety applications. Before my current roles, I worked at Magnite building reinforcement learning systems for programmatic advertising that generated millions in incremental revenue.

I'm passionate about bridging frontier AI research with production systems that deliver real impact. I've previously published in journals including Acta Materialia and Computational Materials Science, and my current Stanford work is funded by Google Cloud Research and targets publication at CogSci and Interspeech conferences.

Through my blog, I write about technical approaches to machine learning - from fine-tuning large language models to deploying ML systems at scale. I enjoy tackling both the research challenges of developing novel architectures and the engineering challenges of shipping reliable systems to production.

Outside of work, I stay active at the gym, train for running events, and explore San Francisco's food and music scene.

Learn more about me through [my LinkedIn](https://www.linkedin.com/in/ajey-venkataraman/), [my Google Scholar profile](https://scholar.google.com/citations?user=DGuRTZ4AAAAJ&hl=en&authuser=1), and [a blog post about my work](https://www.magnite.com/blog/day-in-the-life-ajey-venkataraman-data-scientist/).

Check out my [Blog](/blog/) for technical deep-dives and updates.

## Recent Blog Posts

<ul class="recent-posts">
  {% for post in site.posts limit:5 %}
    <li class="post-preview">
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </li>
  {% endfor %}
</ul>

<a href="/blog/" class="view-all-posts">View all posts →</a>