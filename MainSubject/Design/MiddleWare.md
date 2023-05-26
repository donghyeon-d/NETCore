# 미들웨어

## 기능
* 클라이언트는 로그인 이후부터 매 요청때마다 앱버전, 마스터데이터 버전, Player id, AuthToken 을 보냄
* 컨트롤러의 동작 전에 미들웨어에서 이에 대한 유효성 검사를 함
* 클라이언트 앱 버전 체크
* 클라이언트 마스터 데이터 버전 체크
* 클라이언트 인증 정보 체크

## 로직 
* 클라이언트 앱 버전 체크
* 클라이언트 마스터 데이터 버전 체크
(서버는 앱 버전과 마스터데이터 버전에 대한 정보는 메모리에 갖고 있음)
* Redis에 저장된 player 정보를 가져옴
* 클라이언트가 보낸 Player id, AuthToken와 Redis에 있는 정보를 비교함
* Redis에서 가져온 정보들을 컨트롤러에서 사용할 수 있게 http request정보에 담아놓음

## 사용 DB
### Redis
* Data Type : String
* Key : "P" +playerId + "Info"
* Value : { string AuthToken, int Id, string Status, int CurrentStage }