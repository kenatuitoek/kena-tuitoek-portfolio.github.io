---
layout: archive
title: "Sitemap"
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

### Portfolio
{% for post in site.portfolio reversed %}
- [{{ post.title }}]({{ base_path }}{{ post.url }})
{% endfor %}

### Research
{% for post in site.research reversed %}
- [{{ post.title }}]({{ base_path }}{{ post.url }})
{% endfor %}

### Pages
- [CV](/cv/)
