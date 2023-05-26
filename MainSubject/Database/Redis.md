# Database

# Redis

## 플레이어 관련
### 키 + 값
* 키 : "P" + playerId + "Info"
* 값 : { string AuthToken, int PlayerId, string Status, int CurrentStage }
* 데이터 타입 : String
### 사용
* 로그인 할 때 AuthToken를 발급하여 클라이언트에게 보내줌과 동시에 redis에 저장함. 이후의 모든 요청에 대해서는 playerId와 AuthToken을 비교하여 클라이언트임을 확인함 (미들웨어에서 구현)
* Status : 로그인, 로그아웃, 던전플레이로 나누어, 플레이어의 상태를 저장함


## 공지 관련
### 키 + 값
* 키 : "NoticeKey"
* 값 : [{string Title, string Content, dateTime Date}, {...} ]
* 데이터 타입 : List
### 사용
* 공지 등록은 운영진 계정으로 로그인 했을 때만 가능 (config에 운영진 계정 등록)
* 공지 등록은 List에 LPUSH 함. 이렇게 해야 최근 등록이 인덱스 0에 있음
* 플레이어가 공지 요청시 redis에서 전체 공지를 가져와서 공지 정보를 전달해줌

## 던전스테이지 관련
### 키 + 값
* 키 : "P" +playerId + "Dungeon";
* 값 : { [{int NPCCode, int Count, int Max }, { int NPCCode, int Count, int Max }, ...], [{ int ItemCode, int Count, int Max }, { int ItemCode, int Count, int Max }, ...] }
    * 플레이어가 입장해있는 던전에 나오는 NPC와 Item의 종류와 개수
* 데이터 타입 : String
### 사용
* 플레이어가 던전에 들어갔을 때 이 정보를 redis에 저장함
* NPC를 잡거나 item을 획득 할 때마다 클라이언트의 request가 오고, 서버는 해당 값을 변경하여 위의 값을 바꿈
* 던전이 완료되었을 때, 위에 등록된 모든 NPC에 대해서는 Count == Max가 되어야 하며, item은 Count만큼 플레이어의 아이템리스트에 추가됨
