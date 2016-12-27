## View, Mixin(CBV)

#### generic `View`
```python
# login (FBV)

from django.core.urlresolvers import reverse
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login as auth_login


def login(request):

    if (request.method == "POST"):
        username = request.POST.get("username")
        password = request.POST.get("password")

        next_page = request.POST.get("next_page") or reverse("auth:mypage")
        user = authenticate(username=username, password=password)
        
        if user:
            auth_login(request, user)
            return redirect(next_page)
        return redirect(reverse("auth:login"))

    return render(
        request,
        "auth/login.html",
        {},
    )
```

```python
# LoginView (CBV)

from django.core.urlresolvers import reverse
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login
from django.views.generic import View


class LoginView(View):

    def get(self, request, *args, **kwargs):
        return render(
            request,
            "auth/login.html",
            {},
        )

    def post(self, request, *args, **kwargs):
        username = request.POST.get("username")
        password = request.POST.get("password")

        next_page = request.POST.get("next_page") or reverse("auth:mypage")

        user = authenticate(username=username, password=password)

        if user:
            login(request, user)
            return redirect(next_page)
        return redirect(reverse("auth:login"))
```
- `View` 클래스의 역할은 `POST`, `GET` 구분
- 조건문을 사용할 필요가 없다.

#### `Mixin` 사용하기

```python
# mypage (FBV)

from django.shortcuts import render
from django.contrib.auth.decorators import login_required


@login_required
def mypage(request):
    return render(
        request,
        "auth/mypage.html",
        {},
    )
```

```python
# MypageView (CBV)

from django.shortcuts import render
from django.contrib.auth.mixins import LoginRequiredMixin
from django.views.generic import View


class MypageView(LoginRequiredMixin, View):
    
    def get(self, request, *args, **kwargs):
        return render(
            request,
            "auth/mypage.html",
            {},
        )
```
- CBV 에서는 `login_required` 데코레이터를 바로 사용할 수 없다.
- CBV 에서는 `login_required` 데코레이터와 비슷한 역할을 하는 `LoginRequiredMixin` 을 상속받아서 사용할 수 있다.
