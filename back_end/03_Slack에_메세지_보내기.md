## Slack에 메세지 보내기

#### Code
```python
import requests
import json

# str/json => dict (json.loads)
# dict => str/json (json.dumps)

# JSON => JavaScript Object Notation
# dict => key, value

data = {
	"text": "Hello World",
    "username": "lioliolio",
    "icon_emoji": ":ghost:",
}

response = requests.post("https://hooks.slack.com/services/.../",
						data=json.dumps(data), # Slack은 JSON 형태의 데이터를 받는다 ( Dict X)
                        					   # SMS 의 경우에는 unlencoded 로 dict 을 받는다
			)
```