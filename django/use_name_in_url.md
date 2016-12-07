##url에서 name 사용하기

#### url 함수에 name 사용하기
```
# blog/templates/header.html
<header>
    <h1>Header</h1>
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/news/">News</a></li>
    </ul>
</header>

# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import home, news


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home),
    url(r'^news/$', news"),
]

# news의 url을 변경할 경우 urls.py, header.html 둘 다 수정을 해줘야 한다. 수정해야하는 파일이 많으면 많을수록 같은 작업 계속 반복해서 해야한다.

# 이때 Django에서는 template tag를 이용하여 직접 url을 입력하는 대신 이름을 사용할 수 있다.
```
```
# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import home, news


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^news/$', news, name = "news"),
]


# blog/templates/header.html
<header>
    <h1>Header</h1>
    <ul>
        <li><a href="{% url "home" %}">Home</a></li>
        <li><a href="{% url "news" %}">News</a></li>
    </ul>
</header>

# url에 name을 설정하면 {% url "name" %} 형식의 template tag를 이용하여 url을 불러올수 있다.

# 이렇게 사용할 경우 urls.py만 수정하면 되므로 의존성을 낮출수 있다.
```
