## SMS API 를 이용하여 문자 발송하기

API Test/Client => **Postman**, paw, ..  
**Postman을 사용**

#### Code
```python
import requests

response = requests.post("http://api.openapi.io/ppurio/1/message/sms/id")

response.status_code  # 403 Frobidden

headers = {
	"x-waple-authorization": "key_value",
}

response.status_code  # 500 (4XX => send_phone, dest_phone, msg_body)

data = {
	"send_phone": "01011111111",
    "dest_phone": "01022222222",
    "msg_body": "Hello World",
}

response = requests.post("http://api.openapi.io/ppurio/1/message/sms/id",
						headers=headers,
						data=data,)

response.status_code     # 200
```

#### 함수형태

```python
def send_sms(send_phonenumber, dest_phonenumber, content):
	data = {
    	"send_phone" : send_phonenumber,
        "dest_phone" : dest_phonenumber,
        "msg_body" : content,
    }

    headers = {
	"x-waple-authorization": "key_value",
	}

	response = requests.post(
    	"http://api.openapi.io/ppurio/1/message/sms/id",
    	data=data,    # dict (unlencoded => requests ), str( Slack Message )
                  	  # data=json.dumps(data)
    	headers=headers
    )

    return response

def send_sms_myself(content):
	my_phonenumber = "01011111111"
    return send_sms(my_phonenumber, my_phonenumber, content)
```
회원가입이나 신청 시에 활용 가능