# 던전 리스트 확인
## 기능
* 던전 스테이지는 단계 순서대로 클리어할 수 있음
* 클라이언트가 완료한 스테이지를 확인할 수 있어야 함

## 로직 
* Mysql에는 각 테마별로 완료한 최고 단계 목록을 저장해놓음
* 요청시 Mysql에서 player가 완료한 최고 단계 던전 목록을 불러옴
* 응답으로 보냄

## 사용 DB
### Mysql
* GameDB.CompletedDungeon

## API
> POST /StageList
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "CompleteStage" : {
        "PlayerId" : "int",
        "ForestThema" : "int",
        "BeachThema" : "int",
        "DesertThema" : "int"
    }
}
```

# 던전 선택
## 기능
* 클라이언트가 입장하기 원하는 던전을 선택함
* 클라이언트가 게임 중인 상태로 만들고, 해당 던전에서 잡을 NPC목록과 얻을 수 있는 아이템 목록을 반환해줌
* 던전 플레이 로직은 구현하지 않음

## 로직 
* 들어갈 수 있는 던전인지 확인(이전 스테이지를 돌파 했는지)
* 던전 플레이 정보(NPC목록, 파밍 아이템 목록)를 Redis에 저장함
* player의 상태를 던전플레이 중으로 Redis에 업데이트

## 사용 DB
### Mysql
* GameDB.CompletedDungeon
### Redis
* Data Type : String
* Key : "P" +playerId + "Info"
* Value : { string AuthToken, int Id, string Status, int CurrentStage }

## API
> POST /SelectStage
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "StageCode" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "ItemList" : [
        {
            "ItemCode" : "int",
            "Count" : "int",
            "Max" : "int"
        }
    ],
    "NPCList" : [
        {
            "NPCCode" : "int",
            "Count" : "int",
            "Max" : "int"
        }
    ]
}
```



# NPC 사냥
## 기능
* 클라이언트는 던전 플레이 중에 NPC 한마리 잡을 때마다 API를 보냄
* 서버는 유효한 사냥인지 확인하고 기록함

## 로직 
* 플레이어가 던전 플레이 상태인지, 요청받은 NPC가 유효한 NPC인지 확인
* Redis에서 던전 플레이 정보를 가져옴
* 잡은 NPC를 던전 플레이 정보에 업데이트 함

## 사용 DB
### Redis
* Player Info
    * Data Type : String
    * Key : "P" +playerId + "Info"
    * Value : { string AuthToken, int Id, string Status, int CurrentStage }
* InDungeon
    * Data Type : String
    * Key : "P" +playerId + "Dungeon";
    * Value : { [{int NPCCode, int Count, int Max }, { int NPCCode, int Count, int Max }, ...], 
            [{ int ItemCode, int Count, int Max }, { int ItemCode, int Count, int Max }, ...] }

## API
> POST /KillNPC
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "KilledNPCCode" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
}
```



# 파밍 아이템 획득
## 기능
* 클라이언트는 던전 플레이 중에 아이템을 획득할 때마다 API를 보냄
* 서버는 유효한 아이템 획득인지 확인하고 기록함

## 로직 
* 플레이어가 던전 플레이 상태인지, 요청받은 item이 획은 가능한 item인지 확인
* Redis에서 던전 플레이 정보를 가져옴
* 획득한 item을 던전 플레이 정보에 업데이트 함

## 사용 DB
### Redis
* Player Info
    * Data Type : String
    * Key : "P" +playerId + "Info"
    * Value : { string AuthToken, int Id, string Status, int CurrentStage }
* InDungeon
    * Data Type : String
    * Key : "P" +playerId + "Dungeon";
    * Value : { [{int NPCCode, int Count, int Max }, { int NPCCode, int Count, int Max }, ...], 
            [{ int ItemCode, int Count, int Max }, { int ItemCode, int Count, int Max }, ...] }

## API
> POST /FarmingItem
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "ItemCode" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
}
```


# 던전 스테이지 완료
## 기능
* 던전에 있는 모든 NPC를 잡아야 던전 스테이지 완료 가능
* 스테이지가 완료되면 획득한 아이템, Exp를 지급 함

## 로직 
* player가 던전 플레이 중이고, 요청 받은 스테이지와 플레이 중인 스테이지를 확인함
* Mysql 완료한 던전 목록에 해당 스테이지를 추가함
* 획득한 아이템을 mysql item list에 추가함
* 획득한 돈과 Exp 를 mysql player 정보에 추가함
* 던전이 끝났으니 Redis에 저장했던 플레이어 상태를 변경함

## 사용 DB
### Mysql
* GameDB.Player
* GameDB.Item
* GameDB.CompletedDungeon
### Redis
* Player Info
    * Data Type : String
    * Key : "P" +playerId + "Info"
    * Value : { string AuthToken, int Id, string Status, int CurrentStage }
* InDungeon
    * Data Type : String
    * Key : "P" +playerId + "Dungeon";
    * Value : { [{int NPCCode, int Count, int Max }, { int NPCCode, int Count, int Max }, ...], 
            [{ int ItemCode, int Count, int Max }, { int ItemCode, int Count, int Max }, ...] }

## API
> POST /StageComplete
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "Stage" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "RewardList" : [
        {
            "ItemCode" : "int",
            "Count" : "int",
            "Max" : "int"
        }
    ]
}
```