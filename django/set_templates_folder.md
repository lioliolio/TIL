## templates 폴더 설정하기

```python
# blog/blog/settings.py

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [
            os.path.join(BASE_DIR, "fastube", "templates"),
        ],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
- 앱이 여러 개 존재할 경우 해당 앱을 `INSTALLED_APPS`에 넣는다면 어디서든 template 파일을 불러올 수 있다.
- 프로젝트 이름과 같은 앱(위의 경우 blog)에는 일반적으로 기능을 구현하기 보다는 공통적으로 들어가는 template 파일이나 static 파일, settings 설정 등이 있다. 따라서 `INSTALLED_APPS`에 넣지 않는 경우가 많다.
- 이럴 경우 `blog` 앱에 있는 template 파일을 불러오기 위해서 `settings.py` 에 `TEMPLATES` 부분에서 `DIRS`에 templates 파일이 저장되어 있는 경로를 지정해준다. 그러면 `blog` 앱을 `INSTALLED_APPS`에 넣지 않아도 templates 파일을 불러올 수 있다. 
