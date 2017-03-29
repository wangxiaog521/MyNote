{% for post in site.posts %}
[post.id]({{ site.baseurl }}{{ post.url }})
{% endfor %}
