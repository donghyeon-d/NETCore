# 메일 조회
## 기능
* mysql에 저장되어 있는 메일을 페이지 단위로 불러와서 클라이언트에게 반환함

## 로직 
* 클라이언트에게 받은 페이지 번호를 기준으로 mysql에서 메일을 불러옴
    * 반환해줄 데이터만 select해서 요청함
    * playerId, 만료기간, 삭제되지 않은 것, 페이지 단위 개수만 mysql에서 가져옴
* 응답 반환

## 사용 DB
### Mysql
* GameDB.Mail

## API
> POST /ReadMailList
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "ListNumber" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "Mails" : [
        {
            "MailId" : "Int32",
            "Title" : "String",
            "PostDate" : "DateTime",
            "ExpiredDate" : "DateTime",
            "IsOpened" : "Boolean",
            "IsReceivedItem" : "Boolean",
            "CanDelete" : "Boolean",
            "Sender" : "String",
            "ItemCode" : "Int32",
            "ItemCount" : "Int32"
        }
    ]
}
```

# 특정 메일 내용 보기
## 기능
* 메일의 세부 내용 반환

## 로직 
* 클라이언트가 메일의 상세페이지를 요청함
* mysql에서 해당 메일의 내용을 읽어옴
* 응답을 반환함

## 사용 DB
### Mysql
* GameDB.Mail

## API
> POST /ReadMailContent
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "MailId" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "MailContent" : [
        {
            "MailId" : "Int32",
            "Content" : "String"
        }
    ]
}
```

# 메일 아이템 수령
## 기능
* 메일에 속해 있는 아이템을 수령함
* 해당 아이템을 player의 item list에 저장함

## 로직 
* 요청 받은 메일 번호가 유효한지 확인(플레이어 소유, 아직 안받음)
* 메일 아이템 받음으로 표시
* 아이템을 player의 item list에 저장
* 응답 반환

## 사용 DB
### Mysql
* GameDB.Mail

## API
> POST /ReceiveMailItem
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "MailId" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode"
}
```


# 메일 삭제
## 기능
* 플레이어의 메일 삭제
* DB에서 실제로 삭제하지 않고 논리적으로 삭제함
* DB에 요청할 때, Mail Id, Player Id, Can Delete의 조건에 모두 밪는 것에 대해서만 실행할 수 있게 함 

## 로직
* 클라이언트에게 삭제할 Mail Id를 요청받음
* GameDB.Mail의 데이터에 Mail Id, Player Id, Can Delete의 조건에 모두 맞는 것에 대해서 IsDeleted 요소를 true로 업데이트 함
* 이후 클라이언트가 메일 리스트를 요청할 때, IsDeleted로 체크된 메일은 반환하지 않게 됨

## 사용 DB
### Mysql
* GameDB.Mail

## API
> POST /DeleteMail
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
    "MailId" : "int"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode"
}
```
