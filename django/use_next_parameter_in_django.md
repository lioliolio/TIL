## next parameter 를 이용하여 로그인 후 페이지 바로가기 구현

```python
# blog/views/posts/new.py

from django.contrib.auth.decorators import login_required
from django.shortcuts import render


@login_required
def new(request):
    return render(
        request,
        "posts/new.html",
        {},
    )
```
- `login_required` 데코레이터를 사용하면 로그인을 하지 않고 해당 url로 접근 시 로그인 페이지로 이동한다.
- `/posts/new/` 로 접속시 위의 함수를 실행한다고 가정하자.
- 이 때 위의 url에 접근하면 로그인 페이지로 이동하는데 그 때 url을 보면 `http://localhost:8000/login/?next=/posts/new/` `next parameter` 에 `/posts/new/` 가 들어가 있다.

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
            return redirect(reverse("auth:mypage"))
        return redirect(reverse("auth:login"))

    return render(
        request,
        "auth/login.html",
        {},
    )
```
- `next parameter` 값을 가지고 오기 위해서는 `request.GET.get("next")` 로 가지고 와야 한다.
- 문제는 위의 로그인 함수에서는 조건문 때문에 가지고 올 수가 없다.

```html
<!-- blog/templates/auth/login.html -->

{% extends "base.html" %}

{% block content %}
    <h1>Login</h1>
    
    <form method="POST" action="{% url "auth:login" %}">
        {% csrf_token %}
        <input type="hidden" name="next_page" value="{{ request.GET.next }}">
        <input type="text" name="username" placeholder="username" required>
        <input type="password" name="password" placeholder="password" required>
        <input type="submit" value="로그인">
    </form>
{% endblock %}
```
- `next parameter` 값을 로그인 페이지에 hidden 필드에 넣는다.
- 그렇다면 로그인 함수에서도 문제없이 가지고 올 수 있다.

```python
# 최종 로그인 함수

from django.core.urlresolverse import reverse
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
- hidden 필드에 `next parameter` 값이 있기 때문에 `request.POST.get("next_page")` 로 해당 값을 가지고 올 수 있다.
