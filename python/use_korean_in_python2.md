## Python2 에서 한글 사용하기

#### Python 2 의 한글 입출력 문제점
- Python 2 의 기본 인코딩은 `ASCII`
- 이 문제를 해결하기 위해서는 `# -*- coding: utf8 -*-`을 파일 상단부에 명시해야 한다.
```python
# -*- coding: utf8 -*-

print "한글"
```
#### Python 2 에서 한글을 unicode로 변경할 때 생기는 문제점
- Python 에서는 `str`, `unicode` 두 가지 데이터 타입을 제공한다.
- `unicode` 는 표준 문자열 집합이고 `utf-8`은 `unicode`를 표현하기 위한 방식 중 한가지이다.
```python
# two.py

# -*- coding: utf8 -*-

print unicode("한글")
```
```
$ python two.py
traceback (most recent call last):
  File "two.py", line 3, in <module>
      print unicode("한글")
UnicodeDecodeError: 'ascii' codec can't decode byte 0xed in position 0: ordinal not in range(128)
```
- `unicode`로 decoding 할 때 무슨 방식으로 decoding 할지 명시를 안해주었기 때문에 에러가 생긴다.
- 따라서 decoding, encoding 할 때는 항상 어떤 방식으로 하는지 명시를 해줘야 한다.

```python
# -*- coding: utf8 -*-

print "한글".decode("utf-8")
print "한글".decode("utf-8").encode("utf-8")
```
#### 한글 인코딩 변환하기 - 라이브러리
- Python 의 기본 인코딩을 `ASCII`에서 `utf-8`로 변경해준다.
```python
import sys
reload(sys)
sys.setdefaultencoding('utf-8')
```
#### 한글 인코딩 변환 해결하기
- 파일 상단에 `# -*- coding: utf8 -*-` 명시
- 파이썬 스크립트 내에서는 반드시 `unicode`로 변경해서 사용
- 외부 파일을 읽거나 쓸 때는 `str`로 변경해서 읽거나 사용
- 외부 라이브러리를 사용할 때는`setdefaultencoding`을 사용해서 기본적으로 `utf8`을 사용
