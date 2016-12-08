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
[Writing custom django-admin commands(공식문서)](https://docs.djangoproject.com/en/1.10/howto/custom-management-commands/)
