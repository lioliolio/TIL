## django-pipeline을 사용하여 static file 관리하기

#### `django-pipeline` 이란?

- `django-pipeline` 은 `static file`을 관리, 처리해주는 python library 이다.
- `django`에서는 `collectstatic`이라는 명령어로 앱별로 흩어져 있는 `static file`들을 한번에 `STATIC_ROOT`에 모아주는 명령어를 지원한다. 하지만, 이정도 기능만으로는 부족하다.
- 각 브라우저 별로 한번에 요청을 보낼 수 있는 횟수는 제한되어 있다. `static file`이 많다면 그만큼 속도면에서 불리해 진다.
- 이때 `django-pipeline`을 사용하게 되면, 많은 `static file`들을 하나의 파일로 묶어 줄 뿐만 아니라, `minify`, `uglify`까지 해준다. 따라서 성능 및 코드 보안에 더 좋다.

#### `django-pipeline` 설정하기

- `django-pipeline` 설치하기

```
$ pip install django-pipeline
```

- `INSTALLED_APPS`에 설정

```python
# settings.py

INSTALLED_APPS = [
    'pipeline',
]
```

- `STATIC_DIR` 설정

```python
# settings.py

STATIC_ROOT = os.path.join(PROJECT_ROOT_DIR, 'dist', 'static')
```

- `django-pipeline` 설정하기

```python
# settings.py

STATICFILES_STORAGE = 'pipeline.storage.PipelineCachedStorage'

STATICFILES_FINDERS = (
    'django.contrib.staticfiles.finders.FileSystemFinder',
    'django.contrib.staticfiles.finders.AppDirectoriesFinder',

    'pipeline.finders.PipelineFinder',
)
```

- 위와 같이 설정하면 `django template tag` 대신 `django pipeline template tag`를 사용 할 수 있다.
```html
{% load pipeline %}
{% stylesheet "blog" %}
{% javascript "scripts" %}
```

```python
PIPELINE = {
    'STYLESHEETS': {
        'blog': {
            'source_filenames': (
              'css/application.css',
              'css/partials/*.css',
            ),
            'output_filename': 'css/blog.css',
        }
    }
}
```
- 위와 같이 설정을 하게 되면 `source_filenames`에 있는 `css` 파일들을 `blog.css` 하나의 파일로 묶어서 `STATIC_ROOT` 경로에 저장을 한다.
- 또한 파일 이름 뒤에 해싱한 값을 붙여서 브라우저 캐싱으로 인해 불러오지 못하는 경우를 막아주는 역할도 한다.
