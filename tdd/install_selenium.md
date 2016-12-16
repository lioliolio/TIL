## Selenium 설치하기

```
$ pip install selenium
```
- `webdriver.firefox()` 를 사용하기 위해서는 `geckodriver`가 필요
- [geckodriver](https://github.com/mozilla/geckodriver/releases) 에서 다운로드
- 사용하는 쉘 설정 파일 안에 `geckodriver` path를 설정
```
# .zshrc
export PATH=$PATH:[/path/to/geckodriver]
```
