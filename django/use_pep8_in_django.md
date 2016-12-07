## Django에서 PEP 8 사용하기

#### PEP 8이란?
`PEP 8`이란 Style Guide for Python Code로 파이썬 코드를 작성할 때 사용하는 기준입니다.

* [pep8](https://www.python.org/dev/peps/pep-0008/)

#### pep 8 사용하기
```
# pep8 설치하기
$ pip install pep8

# requirements/development.txt 에 pep8를 넣어 관리할 수 있다.

# pep8 명령어
$ pep8 폴더 또는 파일이름

# pep8 사용 예시 
$ pep8 .
$ pep8 ./blog
```

#### commit 하기 전 pep 8 검사하기
```
$ cp ./git/hooks/pre_commit.samples ./git/hooks/pre_commit

# ./git/hooks/pre_commit
pep8 .

# 위와 같이 저장하면 commit 하기 전에 pep8을 검사하여 틀린 부분이 있으면 commit 되지 않는다.
```

#### pep 8 설정 변경하기
```
# .pep8
[pep8]
max-line-length = 119

# .pep8은 프로젝트 폴더 최상위 (.git, requirements.txt)와 같은 위치에 위치한다.
# 기존 pep8 을 한줄에 79자로 제한되어 있는데 위와 갈이 설정하면 79자에서 119자로 최대 글자수를 늘릴수 있다.
# We allow up to 119 characters as this is the width of GitHub code review
```
