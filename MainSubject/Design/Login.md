# 로그인

## 기능
* 앱 버전, 마스터데이터 버전 확인
* 자신의 게임 데이터 로딩 (기본 게임 데이터, 기본 아이템 데이터)
* 인증키 발급, redis에 저장

## 로직
1. 클라이언트에게 ID, PW를 입력받음
2. 앱 버전, 마스터데이터 버전 확인
3. 로그인 데이터 인증 (AccountDB.Account)
    * 유효한 ID
    * PW 해싱해서 DB에 있는 값과 비교
4. 게임데이터 불러오기
4. 인증 키 생성
5. 인증키, 플레이어 상태 Redis에 등록
5. 인증키, 기본 게임 데이터(GameDB.Player), 아이템 데이터(GameDB.Item) 클라이언트에게 반환

## 사용 DB
### Mysql
* AccountDB.Account (계정 생성)
* GameDB.Player (캐릭터 조회)
* GameDB.Equipment (장착 아이템 조회), GameDB.Inventory(장착하고 있는 아이템 정보 조회), 마스터데이터(item.Name, item.Attribute, item.UseLv, item.MaxStack, itemAttribute.Name)
### Redis
* Data Type : String
* Key : "P" +playerId + "Info"
* Value : { string AuthToken, int Id, string Status, int CurrentStage }

## API
> POST /Login
* request
    
    ``` JSON
    {
        "Email": "string",
        "Password": "string",
        "AppVersion" : "string",
        "MasterDataVersion" : "string"
    }
    ```
* response

    ``` JSON
    {
        "Result" : "ErrorCode",
        "PlayerId" : "int",
        "AuthToken" : "string",
        "Item" : [
            {
                "PlayerId" : "int",
                "ItemId" : "int",
                "ItemCode" : "int",
                "ItemCount" : "int",
                "Attack" : "int",
                "Defence" : "int",
                "Magic" : "int",
                "EnhanceLevel" : "byte",
                "EnhanceTryCount" : "byte",
                "IsDestructed" : "bool",
                "IsDeleted" : "bool"
            }
        ],
        "Player" : {
            "AccountId" : "int",
            "PlayerId" : "int",
            "Exp" : "int",
            "Level" : "int",
            "Hp" : "int",
            "Mp" : "int",
            "Attack" : "int",
            "Defence" : "int",
            "Magic" : "int",
            "Money" : "int"
        }
    }
    ```
