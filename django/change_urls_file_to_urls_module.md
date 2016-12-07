## urls.py를 urls 모듈로 변경하기

```python
# blog/policy_urls.py
from django.conf.urls import url

from blog.views import *


urlpatters = [
    url(r'^policy/terms/$', terms, name="terms"),
    url(r'^policy/privacy/$', privacy, name="privacy"),
    url(r'^policy/disclaimer/$', disclaimer, name="disclaimer"),
]

# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *
from blog.policy_urls import urlpatterns as policy_urlpatterns


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/', include(policy_urlpatterns, namespace="policy")),
]

# policy_urlpatterns를 위와 같이 분리할 수 있다.
# 이 때 django에서는 str으로 urlpatterns를 다음과 같이 읽어올수 있다.

# blog/urls.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/', include("blog.policy_urls", namespace="policy")),
]
```
```python
# blog/urls/__init__.py
from django.conf.urls import url, include
from django.contrib import admin

from blog.views import *


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url(r'^$', home, name="home"),
    url(r'^about/$', about, name="about"),

    url(r'^policy/', include("blog.urls.policy", namespace="policy")),
]

# blog/urls/policy.py
from django.conf.urls import url

from blog.views import *


urlpatters = [
    url(r'^policy/terms/$', terms, name="terms"),
    url(r'^policy/privacy/$', privacy, name="privacy"),
    url(r'^policy/disclaimer/$', disclaimer, name="disclaimer"),
]
# views.py를 views module로 변경하듯이 urls.py도 urls module로 변경할 수 있다.
```
