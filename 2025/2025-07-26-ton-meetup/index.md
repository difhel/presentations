---
layout: article
title:   "TON Builders Meetup"
date:    2025-07-27
summary: "Speeding up UX in TON applications: how to build the perfect frontend for TMA and maximize conversion"
---

{% include_relative README.md %}

{%- comment -%}
  1. figure out this page’s directory
{%- endcomment -%}
{% assign dir = page.path | remove: 'index.md' %}

{%- comment -%}
  2. build a list of all static files in that dir, minus index & README
{%- endcomment -%}
{% assign index_path  = dir | append: 'index.md' %}
{% assign readme_path = dir | append: 'README.md' %}
{% assign files = site.static_files
   | where_exp: "f", "f.path startswith dir"
   | where_exp: "f", "f.path != index_path"
   | where_exp: "f", "f.path != readme_path"
%}

{%- comment -%}
  3. pull out only the first “segment” (so `web/file1…` → `web`)
  and dedupe into the `names` array
{%- endcomment -%}
{% assign names = [] %}
{% for f in files %}
  {% assign relative = f.path | remove_first: dir %}
  {% assign parts    = relative | split: '/' %}
  {% assign name     = parts[0] %}
  {% unless names contains name %}
    {% assign names = names | push: name %}
  {% endunless %}
{% endfor %}

{%- comment -%}
  4. if we found anything, render it
{%- endcomment -%}
{% if names.size > 0 %}
## Files

{% for name in names %}
- [{{ name }}]({{ dir | append: name | relative_url }})
{% endfor %}
{% endif %}
