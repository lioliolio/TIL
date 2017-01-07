## AbstractUser 모델을 상속하여 User 모델 구현하기

```python
# blog/users/models/user.py
# User 모델 사용 시

from django.contrib.auth.models import User
from django.db import models


class UserProfile(models.Model):

    user = models.OneToOneField(User)

    phonenumber = models.CharField(
        max_length=16,
        blank=True,
        null=True,
    )
```
- `User` 모델에 `phonenumber` 필드를 추가하고 싶을 경우 그냥 `User` 모델을 사용한다면 위와 같이 새로운 모델에 `OneToOneField`로 `User` 모델을 연결해서 사용해야 한다.
- 위와 같이 구현을 하게 되면 `User` 모델을 생성시 `UserProfile` 모델이 자동으로 생성되지 않기 때문에 이에 대한 코드를 구현해야 한다.

```python
# blog/users/models/user.py
# AbstractUser 모델을 상속할 경우

from django.contrib.auth.models import AbstractUser
from django.db import models


class User(AbstractUser):

    phonenumber = models.CharField(
        max_length=16,
        blank=True,
        null=True,
    )
```
- `Django`에서는 기존 `User` 모델을 확장할 수 있게 `AbstracUser` 모델을 제공한다.
- `AbstractUser` 모델을 상속받으면 위의 코드 처럼 간단하게 필드를 추가하여 `User` 모델을 확장할 수 있다.

```python
# blog/setting.py

AUTH_USER_MODEL = "users.User"
```
- `AbstractUser` 모델을 상속받아 구현한 `User` 모델을 사용하기 위해서는 위와 같이 `settings.py` 에 `AUTH_USER_MODEL` 을 추가해 주어야 한다. `"users.User"`는 `[User 모델이 있는 App 이름].[User 모델 이름]` 이다.
