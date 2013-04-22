---
layout: default
category: nav
name: index
---

{% for nav in site.nav %}
### {{nav[1]}}

{% assign item = nav[0] %}
{% for list in site[item] %}
* [{{list[1]}}](/{{nav[0]}}/{{list[0]}}.html)
{% endfor %}

{% endfor %}
