# 로그인

## 기능
* 자신의 게임 데이터 로딩 (기본 게임 데이터, 기본 아이템 데이터)
* 앱 버전, 마스터데이터 버전 확인
* 인증키 발급 받음

## 로직
1. 클라이언트에게 ID, PW를 입력받음
2. 앱 버전, 마스터데이터 버전 확인(서버에서 갖고 있는 데이터)
3. 로그인 데이터 인증 (AccountDB.Account)
    * 유효한 ID
    * PW 해싱해서 DB에 있는 값과 비교
4. 인증 키 발급 (Redis에 등록 ID:AuthKEY)
5. 인증키, 기본 게임 데이터(GameDB.Character), 아이템 데이터(GameDB.Equipment) 클라이언트에게 반환


## 로그
1. 요청에 대해
2. 처리 실패시
2. 응답에 대해(응답 종류에 따라)

## 사용 DB
* AccountDB.Account (계정 생성)
* GameDB.Character (캐릭터 조회)
* GameDB.Equipment (장착 아이템 조회), GameDB.Inventory(장착하고 있는 아이템 정보 조회), 마스터데이터(item.Name, item.Attribute, item.UseLv, item.MaxStack, itemAttribute.Name)

## API
* request
    
    `POST /Login`
    ``` JSON
    {
        "ID": "string",
        "PW": "string"
    }
    ```
* response

    `200 OK`
    ``` JSON
    {
        "AuthKey": "string",
        "Character": {
            "Level": "int",
            "Exp": "int",
            "Attack": "int",
            "Defence": "int",
            "Magic": "int",
            "TotalAttack": "int",
            "TotalDefence": "int",
            "TotalMagic": "int"
        },
        "Equipment": {
            "Weapon": {
                "Name": "string",
                "Attribute": "string",
                "UseLv": "int",
                "MaxStack": "int",
                "ItemCount": "int",
                "Attack": "int",
                "Defence": "int",
                "Magic": "int",
                "EnhanceLevel": "int",
                "RemainingEnhanceCount": "int",
                "Destructed": "bool"
            },
            "Shield": "(Weapon과 동일)",
            "Hat": "(Weapon과 동일)",
            "Clothes": "(Weapon과 동일)",
            "Shoes": "(Weapon과 동일)",
            "Glove": "(Weapon과 동일)",
            "Cloak": "(Weapon과 동일)"
        }
    }
    ```
