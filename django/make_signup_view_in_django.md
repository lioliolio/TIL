#### Django 기본 기능으로 회원 가입 만들기

```python
# blog/views/auth/signup.py

from django.core.urlresolvers import reverse
from django.shortcuts import render, redirect
from django.contrib.auth.models import User


def signup(request):
    if (request.method == "POST"):
        username = request.POST.get("username")
        password = request.POST.get("password")
        email = request.POST.get("email")

        user = User.objects.create_user(
            username=username,
            password=password,
            email=email,
        )
        
        return redirect(reverse("auth:login"))

    return render(
        request,
        "auth/signup.html",
        {},
    )
```
- `User.objects.create`로 user 생성시 패스워드 암호화를 하지 않음.
- `User.objects.create_user`롤 user 생성시 패스워드를 암호화 함.
