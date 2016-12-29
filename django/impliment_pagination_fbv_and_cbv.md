## pagination 구현 (FBV, CBV)

#### FBV 에서 pagination 구현

```python
# list.py

from django.shortcuts import render

from blog.models import Post


def list(request):
    page = int(request.GET.get("page", 1))
    per = int(request.GET.get("per", 3))

    start_index = (page - 1) * per
    end_index = page * per

    posts = Post.objects.all()[start_index:end_index]

    return render(
        request,
        "posts/list.html",
        {
            "posts": posts,
        },
    )
```

- `slicing`을 이용해 구현한 `pagination` 이다.
- `Django`에서는 `pagination`을 쉽게 할 수 있는 `Paginator` 라는 클래스를 제공한다.

```python
# list.py ( Paginator 이용 )

from django.core.paginator import Paginator
from django.shortcuts import render

from blog.models import Post


def list(request):
    page = request.GET.get("page", 1)
    per = request.GET.get("per", 3)

    paginator = Paginator(Post.objects.all(), per)
    posts = paginator.page(page)

    return render(
        request,
        "posts/list.html",
        {
            "posts": posts,
        },
    )
```

- `Paginator` 클래스는 `object_list`와 숫자를 받는다.
- `object_list`를 페이지 당 숫자 갯수로 나눈다
- `paginator` 객체에서 `page` 메서드를 사용하면 해당 페이지로 이동이 가능하다.

#### CBV에서 pagination

```python
# get_context_data 에서 pagination

from django.core.paginator import Paginator
from django.views.generic.list import ListView

from blog.models import Post


class PostListView(ListView):
    model = Post
    template_name = "posts/list.html"
    context_object_name = "posts"

    def get_context_data(self, **kwargs):
        context = super(PostListView, self).get_context_data(**kwargs)

        page = self.request.GET.get("page", 1)
        per = self.request.GET.get("per", 3)

        paginator = Paginator(context[self.context_object_name], per)
        context[self.context_object_name] = paginator.page(page)

        return context
```

- `get_context_data` 함수에서 context를 리턴하기 전에 FBV와 같은 방식으로 `pagination`이 가능하다.
- 다만 `get_context_data` 함수는 `context_data`를 전달하는 함수로 이 안에서 `pagination` 기능은 구현하는 건 적합하지 않다.

```python
# get_queryset 에서 pagination

from django.core.paginator import Paginator
from django.views.generic.list import ListView

from blog.models import Post


class PostListView(ListView):
    model = Post
    template_name = "posts/list.html"
    context_object_name = "posts"

    def get_queryset(self):
        queryset = super(PostListView, self).get_queryset()

        page = self.request.GET.get("page", 1)
        per = self.request.GET.get("per", 3)

        paginator = Paginator(queryset, per)
        return paginator.page(page)
```
- `get_queryset` 함수는 `context_data` 중 `object_list` 로 들어갈 `queryset` 을 가져오는 함수이다.
- `get_context_data` 함수보다 더 작은 기능(queryset만 가져오는 기능)을 하기 때문에 위의 함수보다는 `pagination`을 구현하기에 더 적합한 함수이다.

```python
# get_paginate_by 사용

from django.views.generic.list import ListView

from blog.models import Post


class PostListView(ListView):
    model = Post
    template_name = "posts/list.html"
    context_object_name = "posts"

    def get_paginate_by(self, queryset):
        return self.request.GET.get("per", 3)
```

- `ListView` 에서는 `paginate_by`를 사용할 수 있는데 숫자를 넣으면 해당 숫자만큼 `pagination`을 해준다.
- `per` 를 사용하기 위해서 `get_paginate_by` 함수를 위와 같이 사용할 수 있다.
