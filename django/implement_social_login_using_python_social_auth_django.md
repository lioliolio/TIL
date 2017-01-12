## Python Social Auth - Django를 사용하여 소셜 로그인 기능 구현하기

`Python Social Auth` 는 소셜 로그인 기능을 쉽게 구현할 수 있도록 도와주는 파이썬 라이브러리이다. 예전에는 `Django`, `Flask` 등 다양한 프레임워크 기능을 다 포함하고 있었다. 현재는 페이스북, 카카오 등 다양한 백엔드 설정 및 기능 들을 포함하고 있는 `social-auth-core` 라이브러리와 `Django`, `Flask`와 같은 프레임워크마다 설정 및 기능들을 포함하고 있는 라이브러리들로 분리되어 있다.  

## `Python Social Auth - Django` 설치하기

```
$ pip install social-auth-app-django
```
- `social-auth-app-django` 를 설치하면 `social-auth-core`도 같이 설치된다.

## `Python Social Auth - Django` 설정하기

```python
# settings.py

INSTALLED_APPS = [
    ...
    'social_django',
    ...
]
```
- `INSTALLED_APPS` 에 `social_django` 설정

```python
# settings.py

TEMPLATES = [
    {
        'OPTIONS': {
            'context_processors': [
                ...
                'social_django.context_processors.backends',
                'social_django.context_processors.login_redirect',                
                ...
            ],
        },
    },
]
```
- `TEMPLATES` 안에 있는 `context_processors`에 `'social_django.context_processors.backends'`와 `'social_django.context_processors.login_redirect'` 설정

```python
# settings.py

AUTHENTICATION_BACKENDS = [
   "django.contrib.auth.backends.ModelBackend",
]
```
- `AUTHENTICATION_BACKENDS` 설정

```python
# urls.py

from django.conf.urls import include, url
from django.contrib import admin


urlpatterns = [
    url(r'^admin/', admin.site.urls),

    url('', include('social_django.urls', namespace='social')),
]
```
- `urls.py`에 `url('', include('social_django.urls', namespace='social'))`를 설정

```python
# settings.py

SOCIAL_AUTH_PIPELINE = (
    'social_core.pipeline.social_auth.social_details',
    'social_core.pipeline.social_auth.social_uid',
    'social_core.pipeline.social_auth.auth_allowed',
    'social_core.pipeline.social_auth.social_user',
    'social_core.pipeline.social_auth.associate_user',
    'social_core.pipeline.social_auth.load_extra_data',
    'social_core.pipeline.user.user_details',
)
```

- `django-pipeline` 같은 라이브러리를 사용할 경우 `settings` 설정 중 `PIPELINE` 설정이 겹쳐서 제대로 설정 파일들을 못 불러오는 경우가 있다. 이때 `settings` 파일에 위와 같이 `SOCIAL_AUTH_PIPELINE` 설정을 해주면 위의 문제를 해결할 수 있다.

#### 페이스북 로그인 기능 구현하기

```python
# settings.py

AUTHENTICATION_BACKENDS = [
   "social_core.backends.facebook.FacebookOAuth2",

   "django.contrib.auth.backends.ModelBackend",
]

SOCIAL_AUTH_FACEBOOK_KEY = "앱 ID"
SOCIAL_AUTH_FACEBOOK_SECRET = "앱 시크릿 코드"

SOCIAL_AUTH_LOGIN_REDIRECT_URL = "/login/"
```

- [facebook for developers](https://developers.facebook.com/)에서 앱을 만든다.
- 웹주소를 설정하고, `앱 id`는 `SOCIAL_AUTH_FACEBOOK_KEY`에 `앱 시크릿 코드`는 `SOCIAL_AUTH_FACEBOOK_SECTET`에 설정한다.
- `AUTHENTICATION_BACKENDS`에 `"social_core.backends.facebook.FacebookOAuth2"`를 설정한다.
- `SOCIAL_AUTH_LOGIN_REDIRECT_URL`을 설정한다.

#### 카카오 로그인 기능 구현하기

```python
# settings.py

AUTHENTICATION_BACKENDS = [
   "social_core.backends.kakao.KakaoOAuth2",

   "django.contrib.auth.backends.ModelBackend",
]

SOCIAL_AUTH_KAKAO_KEY = "REST API 키"
SOCIAL_AUTH_KAKAO_SECRET = "Admin 키"
```

- [KaKaoDevelopers_](https://developers.kakao.com/) 에서 앱을 만든다.
- `플랫폼 추가`를 하여 웹주소를 설정한다. 그리고 `Redirect Path`에 `/complete/kakao/`를 설정한다.
- `사용자 관리`에서 `사용`에 체크하고 `카카오 계정 연동`에 체크한다.
- `AUTHENTICATION_BACKENDS`에 `"social_core.backends.kakao.KakaoOAuth2"`를 설정한다.
- `SOCIAL_AUTH_KAKAO_KEY`에 `REST API 키`를 `SOCIAL_AUTH_KAKAO_SECRET`에는 `Admin 키`를 설정한다.

- 페이스북, 카카오의 키 값이 깃헙과 같은 공개된 공간에 노출되지 않도록 한다.
