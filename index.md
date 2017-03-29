{% for post in site.posts %}
<li><a href="{{ site.baseurl }}{{ post.url }}">{{ post }}</a></li>
{% endfor %}