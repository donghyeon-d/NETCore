# 공지

## 기능
* 공지는 Redis에 저장됨 (미리 데이터가 들어가있어야 함)
    * `Notice = {title : content, title2 : content2, title3 : content3, ...}`
* 로그인 성공 시 서버에 등록된 공지를 클라이언트에게 전송해야 함 (로그인 정보와 같이 줘도 되고, 클라이언트가 로그인 정보를 받으면 공지 정보를 요청한다고 가정해도 됨)
* 서버 실행 중 공지 변경은 없다
* 공지의 최대 크기는 1K 이다.


## 로직 (로그인 후 클라이언트가 공지 정보를 요청한다고 가정)
1. 클라이언트에게 ID, AuthKey를 받음
2. 앱 버전, 마스터데이터 버전 확인(서버에서 갖고 있는 데이터)
3. 로그인 데이터 인증 (Redis)
    * Key:Value = UserID:AuthKey
4. Redis에서 Notice 정보 불러오기 (RedisKey = Notice)
5. 클라이언트에게 반환


## 로그
1. 요청에 대해
2. 처리 실패시
2. 응답에 대해(응답 종류에 따라)


## 사용 DB
* Redis(UserID, Notice)
* 마스터데이터(item.Name, item.Attribute, item.UseLv, item.MaxStack, itemAttribute.Name)

## API
* request
    
    `POST /Notice`
    ``` JSON
    {
        "ID": "string",
        "AuthKey": "string"
    }
    ```
* response

    `200 OK`
    ``` JSON
    {
        "title" : "content",
        "title2" : "content2",
        "title3" : "content3",
        "..." : "..."
    }
    ```
