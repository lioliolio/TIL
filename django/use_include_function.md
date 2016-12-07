## include 함수 사용하기

```python
# blog/urls.py
from django.conf.urls import url
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/terms/$', terms, name="terms"),
    url(r'^policy/privacy/$', privacy, name="privacy"),
    url(r'^policy/disclaimer/$', disclaimer, name="disclaimer"),

]
# policy의 경우 policy/가 공통으로 들어가므로 그룹을 만들어 줄 수 있다.
# 이때 사용하는 함수는 include 이다.
```
#### include, namespace 사용하기
```python
# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/', include([
        url(r'^policy/terms/$', terms, name="terms"),
        url(r'^policy/privacy/$', privacy, name="privacy"),
        url(r'^policy/disclaimer/$', disclaimer, name="disclaimer"),
    ], namespace="policy")),
]

# include 는 위와 같이 사용할 수 있다.
# url에 name을 설정했듯이 include를 사용하는 경우 namespace를 설정할 수 있다.
```
```html
<footer>
    <h1>Footer</h1>
    <ul>
        <li><a href="{% url "policy:terms" %}">Terms</a></li>
        <li><a href="{% url "policy:privacy" %}">Privacy</a></li>
        <li><a href="{% url "policy:disclaimer" %}">Disclaimer</a></li>
</footer>
<!--namespace를 사용하면 위와 같은 template tag를 사용할 수 있고 그룹별로 관리할 수 있다.-->
```
```python
# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


policy_urlpatterns = [
    url(r'^policy/terms/$', terms, name="terms"),
    url(r'^policy/privacy/$', privacy, name="privacy"),
    url(r'^policy/disclaimer/$', disclaimer, name="disclaimer"),
]

urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/', include(policy_urlpatterns, namespace="policy")),
]

# 위와같이 변수에 리스트를 저장하여 사용할 수 있다.
```
