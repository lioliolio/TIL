## 1:N 관계형(Many TO One)

```python
# post와 comment의 관계를 생각해보자
# 하나의 post에 여러개의 comment를 달 수 있다.
# 따라서 post와 comment의 관계는 1:N 관계라 할 수 있다.
# Django에서는 1:N 관계를 ForeignKey로 정의할 수 있다.


# blog/models/comment.py

from django.db import models


class Comment(models.Model):

    post = models.ForeignKey("Post")

    content = models.TextField()

# Post 와 Comment 의 관계는 위와 같이 ForeignKey로 정의할 수 있다.
# 모델이 같이 앱 안에 있다면 Post 모델을 임포트 하지 않고 "Post"와 같은 방식으로 불러올 수 있다.
```
```
In [1]: post = Post.objects.get(id=1)
In [2]: comment = post.comment_set.all()
Out[2]: [<Comment: wjeifojiwef>, <Comment: weoijfjowiefwef>, <Comment: ㄴ대ㅑ런ㄷㄹ>]
```
- `comment_set`은 related manager로 위와 같은 방식으로 해당 Post 모델 객체와 관련있는 Comment 모델 객체들을 생성, 삭제 등을 할 수 있다.
