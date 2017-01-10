## get_user_model() 사용하기

- `User` 모델을 `AbstractUser` 모델을 상속받아 만들었을 경우, `User` 모델을 불러오기 위해서 `Django` 에서는 `get_user_model()` 이라는 메서드를 제공한다.

```python
# signup.py

from django.core.urlresolvers import reverse
from django.contrib.auth import get_user_model
from django.shortcuts import redirect
from django.views.generic import View


class SignupView(View):

    def get(self, request, *args, **kwargs):
        pass

    def post(self, request, *args, **kwargs):
        username = request.POST.get("username")
        password = request.POST.get("password")

        user = get_user_model().objects.create_user(
            username=username,
            password=password,
        )

        return redirect(reverse("login"))
```

- 위의 코드와 같이 `User` 모델을 따로 임포트 하지 않아도, `get_user_model` 메서드를 사용할 경우, 우리가 생성한 `User` 모델을 불러올 수 있다.
- 위의 `User` 모델은 `settings` 안에 `AUTH_USER_MODEL` 에 설정한 `User`모델을 불러오는 것이다.
