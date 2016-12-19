#### Django 기본 기능으로 admin page 사용하기

## `superuser` 만들기
```
$ python manage.py createsuperuser
```

## Django admin 페이지에서 모델 관리하기
```python
# blog/admin.py

from django.contrib import admin

from blog.models import Post


admin.site.register(Post)
```
- Django 기본 admin 페이지에 `superuser`로 접속시 Post 모델을 admin 페이지에서 관리할 수 있음.
