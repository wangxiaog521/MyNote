{% for post in site.posts %}

* [{{ post.title }}]({{ site.baseurl }}{{ post.url }})

{{ post.id }}
{{ post.url }}
{{ post.title }}
{{ post.id }}

{% endfor %}
