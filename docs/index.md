---
layout: docs
title: Documentation
description: Setup, configuration, and operational guides for Kube Workspaces.
---

{% if site.data.docs %}
  {% for group in site.data.docs %}
<h2>{{ group.title }}</h2>
<div class="docs-cards">
    {% for slug in group.items %}
      {% for doc in site.docs %}
        {% assign doc_slug = doc.path | split: '/' | last | remove: '.md' %}
        {% if doc_slug == slug %}
  <a class="docs-card" href="{{ doc.url }}">
    <div class="docs-card-icon">{% include doc_icon.html slug=doc_slug %}</div>
    <h3>{{ doc.title | default: doc_slug }}</h3>
  </a>
        {% endif %}
      {% endfor %}
    {% endfor %}
</div>
  {% endfor %}
  {% assign unlisted = '' | split: ',' %}
  {% for doc in site.docs %}
    {% assign doc_slug = doc.path | split: '/' | last | remove: '.md' %}
    {% assign is_listed = false %}
    {% for group in site.data.docs %}
      {% for slug in group.items %}
        {% if slug == doc_slug %}{% assign is_listed = true %}{% endif %}
      {% endfor %}
    {% endfor %}
    {% unless is_listed %}
      {% assign unlisted = unlisted | push: doc %}
    {% endunless %}
  {% endfor %}
  {% if unlisted.size > 0 %}
<h2>Other</h2>
<div class="docs-cards">
    {% for doc in unlisted %}
      {% assign doc_slug = doc.path | split: '/' | last | remove: '.md' %}
  <a class="docs-card" href="{{ doc.url }}">
    <div class="docs-card-icon">{% include doc_icon.html slug=doc_slug %}</div>
    <h3>{{ doc.title | default: doc_slug }}</h3>
  </a>
    {% endfor %}
</div>
  {% endif %}
{% else %}
<div class="docs-cards">
  {% assign items = site.docs | sort: 'title' %}
  {% for doc in items %}
    {% assign doc_slug = doc.path | split: '/' | last | remove: '.md' %}
  <a class="docs-card" href="{{ doc.url }}">
    <div class="docs-card-icon">{% include doc_icon.html slug=doc_slug %}</div>
    <h3>{{ doc.title | default: doc_slug }}</h3>
  </a>
  {% endfor %}
</div>
{% endif %}