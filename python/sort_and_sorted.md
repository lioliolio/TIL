## sort()와 sorted()

- 파이썬에서는 리스트를 정렬할 수 있는 함수 두 가지를 제공한다.
- sort()와 sorted() 이다.
- sort()는 리스트 자체를 내부적으로 정렬한다.
- sorted()는 정렬된 리스트 복사본을 반환한다.

```python
# sort()

a = [5, 4, 3, 8, 10]
a.sort()
print(a)    # [3, 4, 5, 8, 10]
```

```python
# sort(ed)

a = [5, 4, 3, 8, 10]
b = sorted(a)
print(b)    # [3, 4, 5, 8, 10]
print(a)    # [5, 4, 3, 8, 10]
```
