{% for post in site.posts %}
* [post.id post.title post.url]({{ site.baseurl }}{{ post.url }})
{% endfor %}
