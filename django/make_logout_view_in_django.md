#### Django 기본 기능으로 로그아웃 만들기

```python
# blog/views/auth/logout.py

from django.core.urlresolvers import reverse
from django.shortcuts import redirect
from django.contrib.auth import logout as auth_logout


def logout(request):
    auth_logout(request)
    return redirect(reverse("home"))
```
