## Vim에 코드 복사, 붙여넣기

#### `:set paste`, `:set nopaste`
- vim 에서 autointent, smartindent 를 사용할 경우 코드를 붙여넣을 때 들여쓰기가 이상하게 된다.
- 이 떄 `:set paste` 명령어를 사용하면 vim 에서 설정해 놓은 옵션을 사용하지 않게 설정할 수 있다.
- `:set paste` 상태에서는 기존 옵션 설정이 작동을 안하기 때문에 항상 코드 복사, 붙여넣기가 끝나면 `:set nopaste` 사용하여 원래 상태로 돌리자.
