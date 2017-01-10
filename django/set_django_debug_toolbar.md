## django-debug-toolbar 설정하기

기존에 사용하던 `django-debug-toolbar 1.4`의 경우 `INSTALLED_APPS` 에 `debug_toolbar` 추가하면 됐다. 하지만 `sqlparser` 버전이 `2.0` 이상이 되면서 오류가 생겨서 최신 버전을 사용하려고 보니 기존보다 복잡해져서 간단하게 정리하기로 한다.  


- `INSTALLED_APPS`에 `debug_toolbar` 추가

```python
# settings.py

INSTALLED_APPS = [
    # ...
    'django.contrib.staticfiles',
    # ...
    'debug_toolbar',
]

STATIC_URL = '/static/'
```

- `MIDDLEWARE` 또는 `MIDDLEWARE_CLASSES`에 `'debug_toolbar.middleware.DebugToolbarMiddleware'` 추가
- `MIDDLEWARE` 는 `Django 1.10` 이상, `MIDDLEWARE_CLASSES` 는 그 아래 버전에서 사용되므로 해당 `Django` 버전에 따라서 설정한다.

```python
# Django 1.10 이상

MIDDLEWARE = [
    # ...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    # ...
]
```

```python
# Django 1.10 이전

MIDDLEWARE_CLASSES = [
    # ...
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    # ...
]
```

- `urls.py`에 아래 내용 추가
```python
# urls.py

from django.conf import settings
from django.conf.urls import include, url

if settings.DEBUG:
    import debug_toolbar
    urlpatterns += [
        url(r'^__debug__/', include(debug_toolbar.urls)),
    ]
```
