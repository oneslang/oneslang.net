---
layout: default
category: index
name: index
---

<div class="row-fluid">

{% for nav in site.nav %}

<div class="span2">
<h3>{{nav[1]}}</h3>
<ul>

{% assign item = nav[0] %}
{% for list in site[item] %}
<li><p><a href="/{{nav[0]}}/{{list[0]}}.html">{{list[1]}}</a></p></li>
{% endfor %}

</ul>
</div>
{% endfor %}

</div>
