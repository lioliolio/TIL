## HTTP METHOD

#### HTTP Method
- GET ( requests.get )
- POST ( requests.post )
- HEAD, OPTION, PUT, PATCH, DELETE ...

#### GET과 POST의 차이
-  GET은 URL Parameter 를 통해서 정보를 넘기는 방식
-  POST는 URL Parameter 를 통해서 정보를 넘기지 않고 HTTP Body 안에 정보를 담아서 보내는 방식이다.(암호화 X)

#### HTTP Method의 역할
- GET => 조회, 검색 ( 데이터의 상태가 바뀌지 않으면서, 정보를 가져올 때 ) ( Retrieve / Read )
- POST => 추가 ( 생성 ) => 웹 상의 리소스가 생길 때 ( Created )
- PUT / PATCH => 데이터가 업데이트 될 때 ( Update )
- DELETE => 데이터가 삭제될 때 ( Destroy )
- CRUD

#### API에 요청할 때, status_code, body
- POST => Successful(201), Failed
- GET => Successful(200), Failed
- Patch ...
- Delete ...

**RESTful 한 설계 (RESful API)가 중요하다**
REST : Representational State Transfer