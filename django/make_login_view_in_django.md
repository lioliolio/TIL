#### Django 기본 기능으로 로그인 만들기

```python
# blog/views/auth/login.py

from django.core.urlresolvers import reverse
from django.shortcuts import render, redirect
from django.contrib.auth import authenticate, login as auth_login


def login(request):
    if (request.method == "POST"):
        username = request.POST.get("username")
        password = request.POST.get("password")

        user = authenticate(username=username, password=password)
        
        if user:
            auth_login(request, user)
            return redirect(reverse("home"))
        return redirect(reverse("auth:login"))

    return render(
        request,
        "auth/login.py",
        {},
    )
```
- `authenticate` 함수는 `username` 과 `password` 를 인자로 받아서 해당 user가 있으면 user를 리턴하고 아니면 None 을 리턴
- `login` 함수는 Django 에서 기본으로 제공하는 함수
- login 여부는 `request.user.is_authenticated` 에서 확인 가능
