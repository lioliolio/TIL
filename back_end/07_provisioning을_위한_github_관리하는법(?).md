## `Provisiong`을 위한 `GitHub` 관리법

#### 개발용 패키지와 배포용 패키지를 구분하자

1. `requirements` 폴더를 생성

2. `development.txt`와 `production.txt` 를 `requirements` 폴더 안에서 생성

3. `production.txt`는 배포용 파이썬 패키지

		# production.txt에는 배포용 파이썬 패키지
		django==1.9.6

4. `development.txt`는 개발용 파이썬 패키지

		# development.txt에는 production.txt의 배포용 파이썬 패키지와 개발용 파이썬 패키지 
		-r production.txt
		ipython

5. `requirements.txt`를 `requirements`의 상위 폴더에 생성

		# requirements.txt에는 배포용 파이썬 패키지
		-r requirements/production.txt

6. 설치

		# 배포용 패키지 설치
		$ pip install -r requirements.txt
