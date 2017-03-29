{% for post in site.posts %}
[post.url]({{ site.baseurl }}{{ post.url }})
{% endfor %}
