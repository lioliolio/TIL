## views.py를 views 모듈로 변경하기

```python
# blog/views.py
from django.shortcuts import render


def home(request):
    return render(
        request,
        "home.html",
        {"site_name": "lioliolio's Blog"},
    )


def about(request):
    return render(
        request,
        "about.html",
        {},
    )
```
```python
# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import home, about


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),
]

# views.py 에 함수가 많아지면 urls.py에서 불러오기가 쉽지 않다.
# views.py가 분리되어 있지 않다면 
# from blog.views import * 로 불러오게 되면 필요하지 않은 함수까지 불러올 수 있다.
# 그렇게 때문에 좋은 방법이 아니다.
```
```python
# blog/views/__init__.py
from .home import home
from .about import about
```
```python
# blog/views/home.html
from django.shortcuts import render


def home(request):
    return render(
        request,
        "home.html",
        {"site_name": "lioliolio's Blog"},
    )
```
```python
# blog/views/about.html
from django.shortcuts import render


def about(request):
    return render(
        request,
        "about.html",
        {},
    )
```
```python
# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),
]
```
```
views.py를 views폴더 안에 함수별로 분리를 해놓을 경우 Django 에서는 views/__init__.py를 읽는다.
__init__.py 안에 사용하는 함수만 넣었다면 
from blog.views import * 로 함수를 불러오더라도 변경하기 전과는 달리 필요한 함수만 불러올 수 있다.
```
