---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
title: FROST Documentation
layout: default
category: main
order: 1
---
# Documentation

The documentation available here:
* [Deployment Architecture](architecture-packages.md)
* [All Configuration Options](settings.md)
* [PostgreSQL setup](postgresql.md)
* [Docker support](docker.md)
* [Authentication Setup](auth.md)

{% assign mydocs = site.pages | group_by: 'category' %}
{% for cat in mydocs %}{% if cat.name.size > 0 %}

## {{ cat.name.length }}{{ cat.name | capitalize }}
{% assign items = cat.items | sort: 'order' %}{% for item in items %}{% if item.title %}
* [{{ item.title }}]({{ item.url }}) {%endif%}{% endfor %}

{%endif%}{% endfor %}


