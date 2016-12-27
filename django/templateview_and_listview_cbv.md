## TemplateView, ListView (CBV)

#### `TemplateView`

```python
# HomeView ( generic View 상속 )

from django.shortcuts import render
from django.views.generic import View


class HomeView(View):

    def get(self, request, *args, **kwargs):
        return render(
            request,
            "home.html",
            {
                "site_name": "blog",
            },
        )
```

```python
# HomeView ( TemplateView 상속 )

from django.views.generic import TemplateView


class HomeView(TemplateView):
    template_name = "home.html"

    def get_context_data(self, **kwargs):
        context = super(HomeView, self).get_context_date(**kwargs)

        context["site_name"] = "blog"
        return context
```

- `TemplateView`는 `GET` 요청시 template 을 렌더링 해준다.
- `template_name` 에 해당 template 이름을 넣으면 된다.
- 만약 위와 같이 바꿔야 하는 문구가 있을 경우 `get_context_data` 함수를 사용하면 된다.

#### ListView

```python
# PostListView

from django.views.generic.list import ListView

from blog.models import Post


class PostListView(ListView):
    model = Post
    template_name = "posts/list.html"
    context_objects_name = "posts"
```

- `ListView`는 `model`을 받는다.
- `TemplateView`와 마찬가지로 `template_name`에 해당 템플릿 이름을 넣으면 렌더링 한다.
- context data의 기본 이름은 `object_list`이다.
- context data의 이름을 바꾸기 위해서는 `context_objects_name` 에 이름을 설정해 주면 된다.
