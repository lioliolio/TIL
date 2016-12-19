## 개발환경에서 static file 관리하기

#### `static file`과 `media file`의 차이
- `static file`은 개발자가 업로드 하는 `css`, `js`, `image`, `file` 등 을 말한다.
- `media file`은 사용자가 업로드하는 `image`, `file` 을 말한다.

```python
# blog/
#   templates/
#   static/
#       css/
#           application.css
#       js/
#           application.js
#       image/
```
- app 폴더 안에 templates 폴더와 같은 위치에 static 폴더를 만들고 그 안에서 css, js 등의 폴더를 만들어서 관리한다.
```html
{% load staticfiles %}<!DOCTYPE=html>
<head>
    <meta charset="utf-8">
    <link rel="stylesheet" href="{% static "css/application.css" %}">
    <script src="{% static "js/application.js" %}"></script>
</head>
```
- `{% load staticfiles %}` 로 `static` template tag를 사용할 수 있다.
- `ie7`에서는 `{% load staticfiles %}` 뒤에 스페이스, 또는 엔터키가 있는 경우 `<!DOCTYPE=html>`를 제대로 읽지 못해서 html 태그가 제대로 동작을 안하는 문제가 있다. 그래서 위와 같이 선언한다.
- template tag를 사용할 수 있기 때문에 static 폴더 안에 css 파일 경로와 js 파일 경로를 위와 같이 사용한다.
- template tag를 사용할 경우 settings 안에 `STATIC_URL` 이 변경이 되더라도 자동으로 해당 css, js 파일을 불러올 수 있다.
