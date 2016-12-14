## Custom Model Manager 만들기

#### Model Manager 란?
- Django ORM 을 사용하여 모델을 생성하거나 삭제할 때에는 `[Model Name].objects.create()` 또는 `[Model Name].objects.delete()`와 같은 방식으로 했다.
- 여기서 `objects`는 Django 내에 구현되어 있는 Model Manager 이다.
- Model Manager는 Model 객체를 생성해주는 객체이다.
- Model Manager를 사용할 경우 기본값을 설정, validation, query 최적화 등을 할수 있다. 따라서 직접 모델 객체를 생성하는 것보다 훨씬 좋은 방식이다.

#### Custom Manager 만들기
```python
from django.db import models


class PostManager(models.Manager):
    pass


class Post(models.Model):

    objects = PostManager()

    title = models.CharField(
        max_length=120,
    )
    content = models.TextField()
    is_public = models.BooleanFiels(
        default = True,
    )
```
- Custom Manager는 `django.db.models.Manager`를 상속받아서 만들 수 있다.
- Custom Manager를 사용할 모델 내에서 Custom Manager 객체를 생성하여 사용할 수 있다.
```
In [1]: Post.objects?
Type:        PostManager
String form: blog.Post.objects
File:        ~/practice/django_project/blog/blog/blog/models/post.py
Docstring:   <no docstring>

In [2]: Comment.objects?
Type:        Manager
String form: blog.Comment.objects
File:        ~/.pyenv/versions/blog/lib/python3.5/site-packages/django/db/models/manager.py
Docstring:   <no docstring>

```
- 위는 Custom Manager를 사용하는 모델이고 아래 모델은 Custom Manager를 사용하지 않고 있다. Type에서 확인이 가능하다.
```python
from django.db import models


class PostManager(models.Manager):
    
    def public(self):
        return self.filter(is_public=True)


class Post(models.Model):

    objects = PostManager()

    title = models.CharField(
        max_length=120,
    )
    content = models.TextField()
    is_public = models.BooleanFiels(
        default = True,
    )
```
- `Post.objects.filter(is_public=True)` 를 Custom Manager 에 `public` method를 선언 함으로 `Post.objects.public()` 로 사용할 수 있다.
