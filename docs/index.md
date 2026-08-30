---
layout: docs
title: Documentation
description: Setup, configuration, and operational guides for Kube Workspaces.
---

Setup, configuration, and operational guides for deploying and running Kube
Workspaces on your Kubernetes cluster. The source lives alongside the
deployment manifests in the
[deploy repository](https://github.com/kube-workspaces/deploy/tree/main/docs).

<div class="docs-cards">
  {% assign items = site.docs | sort: 'title' %}
  {% for doc in items %}
  <a class="docs-card" href="{{ doc.url }}">
    <h3>{{ doc.title | default: doc.name }}</h3>
    <p>{{ doc.excerpt | strip_html | default: 'Guide' }}</p>
  </a>
  {% endfor %}
</div>