---
permalink: /
title: "Quantitative Research & Machine Learning"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I'm **Kena Tuitoek**, an MSc Data Science & Public Policy student at UCL with a background in economics. I work at the intersection of **machine learning, causal inference, and economic/financial applications**.

## Portfolio highlights

{% for post in site.portfolio reversed %}
<div class="portfolio-card" style="margin-bottom: 1.2em; padding: 1em 1.2em; border-left: 3px solid {% if post.accent_color %}{{ post.accent_color }}{% else %}#5B8DEF{% endif %}; background: var(--bg-secondary, rgba(255,255,255,0.02)); border-radius: 0 8px 8px 0;">
  <div style="display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 0.3em;">
    <a href="{{ post.url }}" style="font-size: 1.1em; font-weight: 600; text-decoration: none;">{{ post.title }}</a>
    {% if post.status %}<span style="font-size: 0.7em; font-family: monospace; opacity: 0.6; text-transform: uppercase; letter-spacing: 1px;">{{ post.status }}</span>{% endif %}
  </div>
  <p style="margin: 0; font-size: 0.88em; opacity: 0.7;">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
  {% if post.tags.size > 0 %}
  <div style="margin-top: 0.5em;">
    {% for tag in post.tags %}<code style="font-size: 0.72em; margin-right: 0.4em; padding: 2px 6px; border-radius: 3px; background: var(--bg-secondary, rgba(255,255,255,0.05));">{{ tag }}</code>{% endfor %}
  </div>
  {% endif %}
</div>
{% endfor %}

<p style="margin-top: 1.5em;"><a href="/portfolio/" class="btn btn--primary">View all projects →</a></p>

---

## Looking for 2026 opportunities in

- Machine learning / quantitative research roles  
- Systematic & data-driven roles in finance and tech  
- Research assistant / pre-doc positions in economics and data science  

**Email:** [noelekena@gmail.com](mailto:noelekena@gmail.com) · **LinkedIn:** [kena-tuitoek](https://www.linkedin.com/in/kena-tuitoek/)
