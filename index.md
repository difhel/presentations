---
layout: default
---

<h1>All Presentations</h1>

{% comment %}
  Grab every page that uses layout:article, sort by date descending
{% endcomment %}
{% assign articles = site.pages
   | where:   "layout", "article"
   | sort:    "date"
   | reverse
%}

<div class="articles-grid">
  {% for art in articles %}
    <div class="card">
      <h2><a href="{{ art.url | relative_url }}">
            {{ art.title }}
          </a>
      </h2>
      <p>{{ art.summary }}</p>
      <time datetime="{{ art.date | date_to_xmlschema }}">
        {{ art.date | date: "%B %d, %Y" }}
      </time>
    </div>
  {% endfor %}
</div>
