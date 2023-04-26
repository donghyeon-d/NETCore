# 계정 생성

## 기능
* 아이디, 패스워드 저장
* 아이디 중복체크
* 패스워드 보안
* 캐릭터 생성 기능은 없음
* 기본데이터 생성 (기본 게임 데이터, 기본 아이템 데이터)

## 로직
1. 클라이언트에게 ID, PW를 입력받음
2. ID 중복 체크 (AccountDB.Accout)
3. 패스워드 보안 정책 확인 (대문자, 소문자, 숫자 포함, 10자 이상, ID 겹칩 3자 이하)
4. 패스워드 해시
5. DB에 계정 추가
    * INSERT INTO AccountDB.Accout(ID, PW)
6. 기본 게임 데이터 생성 
    * INSERT INTO GameDB.Character(ID, PW)
    * INSERT INTO GameDB.Equipment(ID, PW)
6. 응답 반환


## 로그
1. 요청에 대해
2. 응답에 대해(응답 종류에 따라)

## 사용 DB
* AccountDB.Account (계정 생성)
* GameDB.Character (케릭터 생성)
* GameDB.Equipment (디폴트 튜플 생성. 계정 이름만)

## API
* request
    
    `POST /CreateAccout`
    ``` JSON
    {
        "ID": "string",
        "PW": "string"
    }
    ```
* response

    `201 Created`
    ``` JSON
    {}
    ```