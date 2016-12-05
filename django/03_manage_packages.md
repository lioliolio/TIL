## Python Package 관리하기

#### 파이썬 패키지를 requirements.txt 로 관리할 수 있다.
```
$ pip install -r requirements.txt
```
#### 개발, 배포 등 다양한 환경에 따른 패키지 관리하기
```
# ~/blog/requirements/production.txt

django==1.9.8
```
```
# ~/blog/requirements/development.txt

-r production.txt
pep8
django-debug-toolbar
```
```
# ~/blog/requirements.txt

-r requirements/production.txt
```
```
# 개발용 패키지 설치
$ pip install -r requirements/development.txt

# 배포용 패키지 설치
$ pip install -r requirements.txt
```
