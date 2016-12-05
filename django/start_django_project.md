## Django Project 시작하기

#### Django Project 만들기
```
$ django-admin startproject ________
```
```
# django-admin startproject blog
# 폴더 구조
blog/
    blog/
        __init__.py 
        settings.py
        urls.py
        wsgi.py
    manage.py
```
#### Django 서버 띄우기
```
$ python blog/manage.py runserver

$ curl localhost:8000 # 웹 브라우져에서도 확인 가능
```
