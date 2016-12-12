## 모델 데이터가 존재할 때 필드 추가하기

```
$ python manage.py makemigrations blog

You are trying to add a non-nullable field 'keyword' to naverpost without a default; we can't do that (the database needs something to populate existing rows).
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows)
     2) Quit, and let me add a default in models.py
     Select an option: 1
     Please enter the default value now, as valid Python
     The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now()
    >>> 1
    Migrations for 'blog':
      0003_naverpost_keyword.py:
          - Add field keyword to naverpost

# NaverPost 라는 모델에 keyword 라는 필드를 추가하고 makemigrations를 했을 때 모델 데이터가 존재 할 경우 위와 같이 나온다.
# 기존 데이터에는 keyword라는 필드가 없었기 때문에 데이터의 일관성을 위해 기존 데이터 keyword 필드에 초기화 값으로 어떤 값을 넣을 지 물어보는 것이다. 
# 위의 경우 1 을 넣었기 때문에 keyword 필드를 추가하기 전 데이터에는 keyword 필드에 1 이 들어가 있다.
```
