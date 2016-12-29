## Django 에서 이미지 파일 업로드 하기

#### model에 `ImageField` 추가
```python
from django.db import models


class Post(models.Model):

    image = models.ImageField(
        blank=True,
        null=True,
    )
```

#### `Pillow` 설치
```
$ pip install Pillow
```
- 운영체제에 따라서 `Pillow` 설치 전에 다른 라이브러리를 설치해야 할 수도 있음.

#### form 수정
```html
<form method="POST" action="{{ action }}" enctype="multipart/form-data>
    {% csrf_token %}
    <input type="file" name="image">
</form>
```
- `form` tag 에 `enctype="multipart/form-data"` 입력

#### view 수정
```python
# blog/views/posts/create.py

from django.shortcuts import redirect

from blog.models import Post


def create(request):
    image = request.FILES.get("image")

    post = Post.objects.create(
        image=image,
    )
    
    return redirect(post)
```
- `image`는 `request.FILES`에서 가져 올 수 있음.

#### MEDIA_ROOT, MEDIA_URL 설정
```python
# settings/partials/static.py

import os

from .base import BASE_DIR


# Media files
MEDIA_ROOT = os.path.join(
    os.path.dirname(BASE_DIR),
    "dist",
    "media",
)
MEDIA_URL = '/media/'
```
- `blog/dist/media` 경로에 이미지 파일 저장

#### URL conf 설정
```python
from django.conf import settings
from django.conf.urls.static import static


urlpatterns = [
] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```
- `static` 함수는 첫 번째 인자 `settings.MEDIA_URL`로 접속할 경우 두 번째 인자 `document_root=settings.MEDIA_ROOT`에서 해당하는 파일을 보여주는 기능을 한다.
