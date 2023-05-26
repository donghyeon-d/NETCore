# 계정 생성

## 기능
* 아이디 중복체크
* 패스워드 보안
* 아이디, 패스워드 저장
* 기본데이터 생성 (기본 게임 데이터, 기본 아이템 데이터)

## 로직
1. 클라이언트에게 ID, PW를 입력받음
2. ID 중복 체크 (AccountDB.Accout)
3. 패스워드 해시
4. DB에 계정 추가
5. 기본 게임 데이터 생성 (계정 정보, player기본데이터, 출석부, 던전 생성)
6. 응답 반환

## 사용 DB
### mysql
* AccountDB.Account (계정 생성)
* GameDB.Player (케릭터 생성)
* GameDB.Item (케릭터 생성)
* GameDB.AttendanceBook (출석부 생성)
* GameDB.CompletedDungeon (완료 던전 정보 생성)

## API
>  POST /CreateAccout
* request
    ``` JSON
    {
        "Email": "string",
        "Password": "string"
    }
    ```
* response
    ``` JSON
    {
        "Result": "ErrorCode"
    }
    ```