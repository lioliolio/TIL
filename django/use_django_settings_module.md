## DJANGO_SETTINGS_MODULE 이용하기
```
$ python manage.py renserver --settings=blog.settings.development
```
위와 같이 명령어를 치는 것은 매우 불편하다. 
```python
## blog/manage.py

#!/usr/bin/env python
import os
import sys

if __name__ == "__main__":
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "blog.settings")

    from django.core.management import execute_from_command_line

    execute_from_command_line(sys.argv)

# manage.py 안에 "blog.settings" 을 "blog.settings.development"로 수정하면
# 뒤에 --settings 없이 개발환경으로 서버를 실행할 수 있다.
# 하지만 좋은 방법이 아니다.
# 개발 환경은 일반적으로 로컬에서만 사용하기 때문이다.
# 이 때 DJANGO_SETTINGS_MODULE 환경 변수를 이용할 수 있다.
```
```
$ export DJANGO_SETTINGS_MODULE = "blog.settings.development"
$ python manage.py runserver

system check identified no issues (0 silenced).
December 08, 2016 - 09:11:19
Django version 1.9.6, using settings 'blog.settings.development'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
Django_SETTINGS_MODULE에 "blog.settings.development"를 저장하면 manage.py를 변경하지 않아도 개발환경으로 서버를 실행할 수 있다.
```
# .env

export DJANGO_SETTINGS_MODULE="blog.settings.development"
```
만약 autoenv를 설치했다면 .env에 export~ 부분을 저장하여 쉽게 사용할 수 있다. 
