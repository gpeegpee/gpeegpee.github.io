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

<h2>Old Tastement</h2>
<hr>
<section id="bible">
  {%for book in site.data.old_tastement %}
    <h3>{{ book.title }}</h3>
    {%for post in site.categories.bible %}
      <ul class="post-list">
      {% if post.tags contain book.title %}
        <li>
          <a href="{{ site.url }}{{ post.url }}">{{ post.title }}
          <span class="entry-date">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
          </span>
          </a>
        </li>
      {% endif %}
      </ul>
    {% endfor %}
  {% endfor %}
</section>

<br>
<h2>New Tastement</h2>
<hr>
<section id="bible">
  {%for book in site.data.new_tastement %}
    <h3>{{ book.title }}</h3>
    {%for post in site.categories.bible %}
      <ul class="post-list">
      {% if post.tags contain book.title %}
        <li>
          <a href="{{ site.url }}{{ post.url }}">{{ post.title }}
          <span class="entry-date">
          <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %d, %Y" }}</time>
          </span>
          </a>
        </li>
      {% endif %}
      </ul>
    {% endfor %}
  {% endfor %}
</section>
