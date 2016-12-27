## DetailView (CBV)

#### `DetailView`

```python
# PostDetailView ( DetailView 상속 )

from django.views.generic.detail import DetailView

from blog.models import Post


class PostDetailView(DetailView):
    model = Post
    template_name = "posts/detail.html"
```
- `ListView` 와 비슷하다.
- context data 이름은 `ListView`와 달리 모델의 소문자( 위의 경우 'post' )로 설정이 된다. 따라서 템플릿에서 'post' 를 사용하고 있을 경우 `ListView`와 같이 설정을 해줄 필요가 없다.
- 다만, url 수정이 필요하다.
```python
# urls/posts.py

from django.conf.urls import url

from blog.views.posts import *


urlpatterns = [
    # url(r'(?P<post_id>\d+)/$', PostDetailView.as_view(), name="detail"),
    url(r'(?P<pk>\d+)/$', PostDetailView.as_view(), name="detail"),
]
```
- `DetailView` 에서는 모델 객체에서 `pk` 또는 `slug` 를 불러온다. 따라서 url 파일에서 위와 같이 `pk`를 불러오거나 `slug`를 불러오도록 변경해야 한다.

