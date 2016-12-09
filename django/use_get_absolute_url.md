## get_absolute_url() 사용하기

아래와 같이 Post 모델 데이터 list를 보여주는 페이지와 세부 내용을 볼 수 있는 detail 페이지가 있는 경우를 생각해보자.
```html
<!--blog/templates/posts/list.html-->

<h1>Post List</h1>
<ul>
    {% for post in posts %}
    <h2>{{ post.title }}</h2>
    <p>{{ post.content }}</p>
    {% endfor %}
</ul>
```
```html
<!--blog/templates/posts/detail.html-->

<h1>{{ post.title }}</h1>
<p>{{ post.content }}</p>
```
```python
# blog/urls/__init__.py

from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^posts/$', list, name="post-list"),
    url(r'^posts/(?P<post_id>\d+)/$', detail, name="post-detail"),
]
```
detail 페이지에 들어가기 위해서는 Post 모델에서 Post id 값을 가져와야 한다. 이 때 list 페이지에서 각 항목 타이틀에 링크를 걸어서 detail 페이지와 연결해보자.

```html
<!--blog/templates/posts/list.html-->

<h1>Post List</h1>
<ul>
    {% for post in posts %}
    <a href="/posts/{{ post.id }}">
        <h2>{{ post.title }}</h2>
    </a>
    <p>{{ post.content }}</p>
    {% endfor %}
</ul>
```
의존성을 낮추기 위해 url에 name을 이용하면 다음과 같이 사용할 수 있다.

```html
<!--blog/templates/posts/list.html-->

<h1>Post List</h1>
<ul>
    {% for post in posts %}
    <a href="{% url "post-detail" post_id=post.id %}">
        <h2>{{ post.title }}</h2>
    </a>
    <p>{{ post.content }}</p>
    {% endfor %}
</ul>
```
현재 템플릿에서 post_id 값을 받아와서 url을 만들고 있는데 이 부분은 model에서 가능하게 하는 method가  get_absolute_url() 이다.
```python
# blog/models.py
from django.db import models


class Post(models.Model):
    title = models.CharField(
        max_length=120,
    )
    content = models.TextField()

    def __str__(self):
        return self.title

    def get_absolute_url(self):
        return return "/posts/ + self.id + "/"
# 위와 같이 정의를 해주는 것은 간단하다. 하지만 url 주소가 변경될 경우 
# model에 정의된 url 주소도 변경해야하므로 일반적으로 위와 같이 쓰이진 않는다.
```
```python
# blog/models.py
from django.db import models
from django.core.urlresolvers import reverse


class Post(models.Model):
    title = models.CharField(
        max_length=120,
    )
    content = models.TextField()

    def __str__(self):
        return self.title

    def get_absolute_url(self):
        return reverse(
            "post-detail",
            kwargs={
                "post_id": self.id,
            }
        )

# reverse 함수를 사용한다.
# reverse 함수는 url에 정의한 name에서 해당 url을 불러온다. 
# 위와 같이 post_id가 필요한 경우 kwargs 에 해당 값을 넣어주면 된다. 
```
```html
<!--blog/templates/posts/list.html-->

<h1>Post List</h1>
<ul>
    {% for post in posts %}
    <a href="{{ post.get_absolute_url }}">
        <h2>{{ post.title }}</h2>
    </a>
    <p>{{ post.content }}</p>
    {% endfor %}
</ul>
```
Post Model에 get_absolute_url을 정의해주면 위와 같이 모델에서 바로 url을 가져올 수 있게 된다.
