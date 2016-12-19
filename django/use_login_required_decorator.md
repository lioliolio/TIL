#### login_required 데코레이터 사용하기

```python
from django.shortcuts import render
from django.contrib.auth.decorators import login_required


@login_required
def new(request):
    return render(
        request,
        "posts/new.html",
        {},
    )
```
- `login_required` 데코레이터를 사용하면 해당 view는 로그인을 해야만 접근 가능.
