---
layout: page
title: Book
description: "Book"
permalink: /book/
comments: false
sitemap: false
noindex: true
category: base
---

<section id="book">
  {%for post in site.categories.book %}
    <ul class="post-list">
      <li>
      <a href="{{ site.url }}{{ post.url }}">{{ post.title }}
      <span class="entry-date">
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
      </span>
      </a>
      </li>
    </ul>
  {% endfor %}
</section>

<!--
<section id="book">
  {%for post in site.categories.book %}
    {% unless post.next %}
      <ul class="post-list">
    {% else %}
      {% capture year %}{{ post.date | date: '%Y' }}{% endcapture %}
      {% capture nyear %}{{ post.next.date | date: '%Y' }}{% endcapture %}
      {% if year != nyear %}
      <h3>{{ post.date | date: '%Y' }}</h3>
      <ul class="post-list">
      {% endif %}
    {% endunless %}
      <li>
      <a href="{{ site.url }}{{ post.url }}">{{ post.title }}
      <span class="entry-date">
      <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
      </span>
      </a>
      </li>
  {% endfor %}
  </ul>
</section> -->
