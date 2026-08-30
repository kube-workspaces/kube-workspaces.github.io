---
layout: docs
title: Documentation
description: Setup, configuration, and operational guides for Kube Workspaces.
---

Setup, configuration, and operational guides for deploying and running Kube
Workspaces on your Kubernetes cluster. The source lives alongside the
deployment manifests in the
[deploy repository](https://github.com/kube-workspaces/deploy/tree/main/docs).

{% if site.data.docs %}
  {% for group in site.data.docs %}
<h2>{{ group.title }}</h2>
<div class="docs-cards">
    {% for slug in group.items %}
      {% for doc in site.docs %}
        {% assign doc_slug = doc.path | split: '/' | last | remove: '.md' %}
        {% if doc_slug == slug %}
  <a class="docs-card" href="{{ doc.url }}">
    <h3>{{ doc.title | default: doc_slug }}</h3>
    <p>{{ doc.excerpt | strip_html | default: 'Guide' }}</p>
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
    <h3>{{ doc.title | default: doc_slug }}</h3>
    <p>{{ doc.excerpt | strip_html | default: 'Guide' }}</p>
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
    <h3>{{ doc.title | default: doc_slug }}</h3>
    <p>{{ doc.excerpt | strip_html | default: 'Guide' }}</p>
  </a>
  {% endfor %}
</div>
{% endif %}