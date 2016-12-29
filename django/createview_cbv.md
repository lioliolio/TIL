## CreateView (CBV)

#### `CreateView`

```python
# PostCreateView

from django.views.generic.edit import CreateView

from blog.models import Post


class PostCreateView(CreateView):
    model = Post
    fields = [
        "title",
        "content",
        "image",
    ]

    def form_valid(self, form):
        form.instance.user = self.request.user
        return super(PostCreateView, self).form_valid(form)
```
- `CreateView`은 `model`과 `field`를 받는다.
- `form_valid` 메서드를 통해서 `user` 정보를 받을 수 있다.

```python
# form_valid 를 이용하지 않을 경우

from django.views.generic.edit import CreateView

from blog.models import Post


class PostCreateView(CreateView):
    model = Post
    fields = [
        "title",
        "content",
        "image",
        "user",
    ]
```

```html
<!-- posts/form.html -->

<form method="POST" action="{{ action }}" enctype="multipart/form-data">
    {% csrf_token %}
    <input type="text" name="title" placeholder="제목" value="{% if post %}{{ post.title }}{% endif %}">
    <input type="text" name="content" placeholder="본문" value="{% if post %}{{ post.content }}{% endif %}">
    <input type="file" name="image">
    <input type="hidden" name="user" value="{{ request.user.id }}">
    <input type="submit" value="Publish">
</form>
```
- 위와 같이 `html form`에 `hidden` 타입으로 유저정보를 넘겨주면 `form_valid` 메서드를 사용하지 않고 같은 기능을 구현할 수 있다.
- 하지만 `user` 정보를 조작할 수 있기 때문에 위와 같은 방식으로 구현하면 안된다!!!

```python
# PostCommentCreateView

from django.views.generic.edit import CreateView

from blog.models import Comment, Post


class PostCommentCreateView(CreateView):
    model = Comment
    fields = [
        "content",
    ]

    def form_valid(self, form):
        form.instance.user = self.request.user
        form.instancel.post = Post.objects.get(
            id=self.kwargs.get("post_id"),
        )

        return super(PostCommentCreateView, self).form_valid(form)
```
- `Comment` 모델은 `Post` 모델과 `1:N` 관계이다.
- `url`에 `post_id` 라는 이름으로 `post id` 값이 있다고 가정하자..
- `post id`값은 `kwargs`에서 찾을 수 있다.
- 위와 같이 해당 `post id` 값을 찾아서 가져올 수 있다.
