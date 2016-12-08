## 개발 환경과 배포 환경 구분하기

#### settings.py를 settings 모듈로 바꾸기
[Github에서 확인](https://github.com/lioliolio/blog_practice/commit/1c128766369d87e6b8e5397271b7bf7a8b69a1a8)
```python
# settings/partials/에 settings.py를 분리
# settings BASE_DIR의 경우 기존 settings.py보다 트리 구조 상 두 단계 더 밑에 있다. 따라서

BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

BASE_DIR = os.path.dirname(os.path.dirname(os.path.dirname(os.path.dirname(os.path.abspath(__file__)))))

# 아래와 같이 변경
# 특정 라이브러리가 필요한 경우 그 라이브러리를 import 시켜주어야 한다.
```
```python
# settings/production.py

from .partials import *


DEBUG = False

ALLOWED_HOSTS = ["*", ]


# 배포 환경의 경우 dubug 모드는 false, 모든 사람이 접속할 수 있게 설정을 해준다. 
```
```python
# settings/development.py

from .partials import *


INSTALLED_APPS += [
    'debug_toolbar',
    'django_extensions',
]

# 개발 환경의 경우 개발 환경에서 사용하는 앱들을 추가해준다.
```
```python
# setttings/__init__.py

from .production import *
```
```
$ python manage.py runserver
```
실행시 배포환경으로 서버가 실행한다.
```
$ python manage.py renserver --settings=blog.settings.development
```
개발환경으로 서버를 실행하고 싶다면 `--settings`에 위의 값을 넣어서 실행하면 된다.
