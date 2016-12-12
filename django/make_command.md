## Django 명령어 만들기

```python
# 폴더 구조

# blog/
#   blog/
#       management/
#           commands/
#               __init__.py
#               hello.py
#       __init__.py
#   views/
#   urls/
# manaage.py

# 명령어 간단한 예
# blog/management/commands/hello.py

from django.core.management.base import BaseCommand


class Command(BaseCommand):
    
    def handler(self, *args, **options):
        self.stdout.write("hello world")
```
```
$ python manage.py hello
hello world
```
```python
# management/commands/ 안에 _로 시작하지 않으면 manage.py 명령어로 등록한다.
# 위의 명령어를 실행하기 위해서는 INSTALLED_APPS에 blog 어플리케이션이
# 포함되어야 한다.
# Command 클래스는 BaseCommand를 상속받는다.
```
#### 명령어에 옵션 사용하기
```python
# blog/management/commands/crawling.py

from django.core.management.base import BaseCommand


class Command(BaseCommand):

    def add_arguments(self, parser):
        parser.add_argument("query", type=str)

    def handle(self, *args, **options):
        query = options.get("query")
        self.stdout.write("{query}을 크롤링 하겠습니다.".format(
            query=query,
        ))

# 위와 같이 add_arguments method를 사용하면 명령어에 옵션을 사용할 수 있다.
```
```
$ python manage.py crawling 박보영
박보영을 크롤링 하겠습니다.
```
[Writing custom django-admin commands(공식문서)](https://docs.djangoproject.com/en/1.10/howto/custom-management-commands/)
