---
layout: page
title: Bible
description: "Bible"
permalink: /bible/
comments: false
sitemap: false
noindex: true
category: base
---

{{ site.oldtastement }}

<section id="bible">
  {%for book in site.old_tastement %}
      {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      <h3>{{ book }}</h3>
      <ul class="post-list">
      {%for post in site.categories.bible %}
      <li>
        <a href="{{ site.url }}{{ post.url }}">{{ post.title }}
        <span class="entry-date">
        <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
        </span>
        </a>
      </li>
      {% endfor %}
      </ul>
  {% endfor %}
</section>
