# Database

# Redis

## 로그인 및 인증 관련
* 첫 로그인시 인증키를 발급하여 클라이언트에게 전달함. 이 인증키는 UserID = 인증키 의 쌍으로 Redis에 저장함
* 로그인 이후의 모든 요청에서 클라이언트는 UserID, 인증키를 바디에 포함하여 보내야함
* 서버는 UserID, 인증키를 받으면 유효한지 Redis에서 인증 검사 후 요청에 대해 처리해줌
``` redis
    UserID = AuthKey
```
