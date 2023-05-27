# 아이템 강화

## 기능
* 강화 최대 횟수 제한이 있어야 함
* 무기와 방어구만 강화 할 수 있음
* 아이템 강화 가능 횟수가 0이면 강화할 수 없음
* 강화 실패시 아이템을 파괴함
* 강화 성공 확률은 30%이며, 성공시 공격력 또는 방어력이 올라가야 함
* 아이템 별로 강화 단계 이력 정보가 있어야 함

## 로직 
* 클라이언트에게 요청 받은 아이템을 Mysql에서 불러옴
* 강화 가능한 아이템인지 확인함
* 강화 가능한 아이템이면 강화 시도
* 강화 결과를 GameDB.Item에 업데이트 함

## 사용 DB
### Mysql
* GameDB.Item

## API
> POST /EnhanceItem
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "string",
    "AppVersion" : "string",
    "MasterDataVersion" : "string",
    "ItemId" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "ResultItem" : {
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
}
```