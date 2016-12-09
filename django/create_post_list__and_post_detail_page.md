## Post List, Detail 페이지 만들기
```python
# blog/urls/__init__.py

from django.conf.urls import url
from django.contrib import admin

from blop.views import *

urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^posts/list/$', list, name="post-list"),
    url(r'^posts/list/(?P<post_id>\d+)/$', detail, name="post-detail"),
]
```
```python
# blog/views/posts/list.py

from django.shortcuts import render

from blog.models import Post


def list(request):
    return render(
        request,
        "posts/list.html",
        {
            "posts": Post.objects.all(),
        },
    )
```
```html
<!--blog/templates/posts/list.html-->

{% extends "base.html" %}

{% block content %}
<h1>Post List</h1>

<ul>
    {% for post in posts %}
    <a href="/posts/{{ post.id }}">
        <h2>{{ post.title }}</h2>
    </a>
    <p>{{ post.content }}</p>
    {% endfor %}
</ul>
{% endblock %}
```
```python
# blog/views/posts/detail.py

from django.shortcuts import render

from blog.models import Post


def detail(request, post_id):
    return render(
        request,
        "posts/detail.html",
        {
            "post": Post.objects.get(id=post_id), 
        },
    )
```
```html
<!--blog/templates/posts/detail.html-->

{% extends "base.html" %}

{% block content %}
<h1>{{ post.title }}</h1>
<p>{{ post.content }}</p>
{% endblock %}
```
