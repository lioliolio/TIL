## Django Signal: post_save signal 사용하기

#### `Signal` 이란?
- 특정 이벤트가 발생했을 때 자동으로 실행되는 메쏘드 또는 함수
- `hook` 이라 부르기도 한다.

#### `post_save` 사용하기
- `post_save` 는 `Django` 에서는 제공하는 여러 `signal` 중 하나이다.
- `model`이 저장 된 이후에 특정 메쏘드 또는 함수를 부르는 `singal` 이다.

```python
# users/models/user_profile.py

from django.contrib.auth.models import User
from django.db import models
from django.db.models.signals import post_save


class UserProfile(models.Model):

    user = models.OneToOneField(User)

    phonenumber = models.CharField(
        max_length=16,
        blank=True,
        null=True,
    )

    address = models.CharField(
        max_length=64,
        blank=True,
        null=True,
    )


def post_save_user(sender, instance, created, **kwargs):
    if created:
        user_profile = UserProfile.objects.create(
            user=instance,
        )

post_save.connect(post_save_user, sender=User)
```

- `post_save_user`는 `User` 모델이 생성될 때 실행하는 함수로 자동으로 `UserProfile` 모델을 생성해준다.
- `post_save signal` 은 `sender, instance, created` 등의 인자를 보내기 때문에 `post_save_user` 파라미터로 위와 같이 설정한다. 공식 문서에 따르면 `def post_save_user(sender, **kwargs):` 라 해도 똑같이 동작한다.
- `post_save.connect` 는 `model(User)`과 `post_save_user` 함수를 연결해 준다.

```python
# users/models/user_profile.py

from django.contrib.auth.models import User
from django.db import models
from django.db.models.signals import post_save
from django.dispatch import receiver


class UserProfile(models.Model):

    user = models.OneToOneField(User)

    phonenumber = models.CharField(
        max_length=16,
        blank=True,
        null=True,
    )

    address = models.CharField(
        max_length=64,
        blank=True,
        null=True,
    )


@receiver(post_save, sender=User)
def post_save_user(sender, instance, created, **kwargs):
    if created:
        user_profile = UserProfile.objects.create(
            user=instance,
        )
```

- `post_save.connect` 대신 `receiver` 데코레이터를 사용할 수 있다.

```python
# users/signals/post_save.py

from django.contrib.auth.models import User
from django.db.models.signal import post_save
from django.dispatch import receiver

from users.models.user_profile import UserProfile


@receiver(post_save, sender=User)
def post_save_user(sender, instance, created, **kwargs):
    if created:
        user_profile = UserProfile.objects.create(
            user=instance,
        )
```

```python
# users/apps.py

from django.apps import AppConfig


class UsersAppConfig(AppConfig):
    name = "users"

    def ready(self):
        from users.signals.post_save import post_save_user
```

```python
# users/__init__.py

default_app_config = "users.apps.UsersAppConfig"
```

- `signals` 모듈로 따로 분리할 경우 위와 같이 `apps.py`와 `__init__.py` 설정을 따로 해줘야 한다.
