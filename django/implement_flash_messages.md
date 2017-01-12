## Flash Messages 구현하기

#### `Flash Message` 란?
- 한 번 웹 상에서 보여주는 메세지 ( 예) 로그인하거나 로그아웃 할 때 나오는 메세지)
- `Django` 에서는 `message framework` 를 제공한다.

```python
# logout.py

from django.contrib import messages
from django.contrib.auth import logout
from django.core.urlresolvers import reverse
from django.shortcuts import redirect
from django.views.generic import View


class LogoutView(View):
    
    def get(self, request, *args, **kwargs):
        logout(request)
        messages.add_message(
            request,
            messages.SUCCESS,
            "성공적으로 로그아웃 되었습니다.",
        )
        return redirect(reverse("home"))
```

- `flash message`를 추가하는 메서드는 `messages.add_message` 이다. `add_messsage` 메서드는 `request`, `level`, `messages`, `extra_tags` 등을 인자로 받는다.
- `level`에는 숫자(인트) 값이 들어가야 하는데 `Django`에서는 기본적으로 `messages.SUCCESS`, `messages.ERROR` 등 기본값들이 제공된다.
- 위의 기본 값들을 사용할 경우 `tags` 값은 이름의 소문자이다. ( 예) `messages.SUCCESS`의 경우 `tags`는 `success` )
- 메세지를 보여주기 위해선 `template` 파일을 설정해야 한다.

```html
{% if messages %}
    <ul>
        {% for message in messages %}
        <li class="{{ message.tags }}">
            <p>{{ messsage }}</p>
        </li>
        {% endfor %}
    </ul>
{% endif %}
```
- `template` 파일 내에서는 위와 같이 불러올 수 있다.
- `template` 파일 밖에서 부르기 위해서는 `get_messages()` 사용하면 된다. 자세한 사항은 [Django messages](https://docs.djangoproject.com/en/1.10/ref/contrib/messages/) 확인 할 수 있다.
