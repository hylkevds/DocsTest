---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
title: FROST Documentation
layout: default
category: main
order: 1
---

# FROST Documentation

These pages contain the documentation for FROST-Server.


{% assign mydocs = site.pages | sort: 'order' | group_by: 'category' %}
{% for category in site.data.categories %}
## {{ category.title }}
{% for catItem in mydocs %}
{% if catItem.name == category.key %}
{% assign items = catItem.items | sort: 'order' %}{% for item in items %}{% if item.title %}
* [{{ item.title }}]({{ site.baseurl }}{{ item.url }}) {%endif%}{% endfor %}
{%endif%}{% endfor %}

{% endfor %}

<ul>
{% assign mydocs = site.pages | sort: 'order' | group_by: 'category' %}
{% for category in site.data.categories %}
	<li class="tag-h1">{{ category.title }}
		<ul>
			{% for catItem in mydocs %}
				{% if catItem.name == category.key %}
					{% assign items = catItem.items | sort: 'order' %}
					{% for item in items %}
						<li class="tag-h2"><a href="{{ site.baseurl }}{{ item.url }}">{{ item.title }}</a>
							{% if item.childCategory %}
								<ul>

								{% for subcatItem in mydocs %}
									{% if subcatItem.name == item.childCategory %}
										{% assign subitems = subcatItem.items | sort: 'order' %}
										{% for subitem in subitems %}
											<li class="tag-h3"><a href="{{ site.baseurl }}{{ subitem.url }}">{{ subitem.title }}</a></li>
										{% endfor %}
									{%endif%}
								{% endfor %}
									
								</ul>
							{%endif%}
						</li>
					{% endfor %}
				{%endif%}
			{% endfor %}
		</ul>
	</li>
{% endfor %}
</ul>

