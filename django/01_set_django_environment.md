## Django 개발 환경 설정

#### 순서
**MAC 을 기준으로 작성**  

1. `pyenv`, `virualenv`, `autoenv` 설치

2. 가상환경 구축

		$ pyenv virtualenv 3.5.1 blog # 파이썬 버전 = 3.5.1, 가상환경 이름 = blog

3. 가상환경 실행

		$ pyenv activate blog # 가상환경이름 = blog

4. `autoenv` 사용

		# ~/my_project/.env 에 이 스크립트 삽입
		pyenv activate blog

5. 패키지 확인

		$ pip freeze

6. `Django` 설치

		$ pip install django==1.9.6
