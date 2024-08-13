---
title: Home
description: HTML Spec. and extensible registry
layout: default
---

# OpenAPI Initiative Registry

This site contains the OpenAPI Initiative Registry and content for the HTML versions of specifications managed by the OpenAPI Initiative such as the OpenAPI Specification and the Arazzo Specification.

## Registry

* Proceed to [Registry](./registry/index.html)

## OpenAPI Initiative Specifications

### Arazzo Specification Versions

{% assign html_files = site.static_files | where: "extname", ".html" | sort: "basename" | reverse %}
{% for file in html_files %}
{% assign segments = file.path | split: "/" %}
{% assign firstchar = file.basename | slice: 0 %}
{% if segments[1] == "arazzo" and file.extname == ".html" and firstchar == "v" %}
* [{{ file.basename }}]({{ site.baseurl }}{{ file.path }})
{% endif %}
{% endfor %}

### OpenAPI Specification Versions

{% assign html_files = site.static_files | where: "extname", ".html" | sort: "basename" | reverse %}
{% for file in html_files %}
{% assign segments = file.path | split: "/" %}
{% assign firstchar = file.basename | slice: 0 %}
{% if segments[1] == "oas" and firstchar == "v" %}
* [{{ file.basename }}]({{ site.baseurl }}{{ file.path }})
{% endif %}
{% endfor %}

### Latest JSON Schemas for OpenAPI Specification Versions

{% assign schema_files = site.static_files | where: "extname", "" | sort: "path" | reverse %}
{% assign last_version = "" %}
{% for file in schema_files %}
{% assign segments = file.path | split: "/" %}
{% if segments[1] == "oas" and file.basename contains "lat" %}
{% if segments[2] != last_version %}
{% assign last_version = segments[2] %}
* v{{ last_version }}
{% endif %}
  * [{{ segments[3] }}]({{ file.path }})
{% endif %}
{% endfor %}
