## Model 생성하기

```python
# blog/models.py

from django.db import models


class Post(models.Model):

    title = models.CharField(
        max_length=120,
    )

    content = models.TextField()

# app/models.py 에 Model을 정의할 수 있다.
# 이 때 앱은 settings 안에 INSTALLED_APPS에 넣어야한다.

# Django에서는 django.db 안에 models 모듈에서 Model을 상속받아 모델을 만들 수 있다.
# models 모듈에는 CharField, TextField 등 데이터를 저장하기 위한 다양한 Field 가 정의되어 있다. 
```
```
>> Post.objects.create(title="제목1", content="본문1")
# Django ORM을 사용한다면 위와 같은 명령어로 모델 안에 데이터를 넣을 수 있다.
```
