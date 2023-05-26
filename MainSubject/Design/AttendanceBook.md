# 출석부 조회
## 기능
* 출석부 정보를 조회함
* 연속일이 몇일인지, 오늘 수령 했는지를 반환함

## 로직 
* mysql에서 player의 출석부 정보를 가져옴
* 출석을 연속으로 했는지의 여부와 출석일수를 계산하여 응답함

## 사용 DB
### Mysql
* GameDB.AttendanceBook

## API
> POST /LoadAttendanceBook
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
    "DayCount" : "int",
    "CanReceive" : "bool"
}
```

# 출석부 보상 받기
## 기능
* 출석 여부와 출석일을 확인하여, 출석 보상 아이템을 메일로 지급함

## 로직 
* mysql에서 출석부 정보를 읽어옴
* 오늘 이미 수령했는지 확인함
* 오늘 출석일 했음으로 mysql에 정보를 업데이트 함
* 메일로 보상을 보냄 (GmailDB.Mail에 보상을 insert함)

## 사용 DB
### Mysql
* GameDB.AttendanceBook
* GameDB.Mail

## API
> POST /ReceiveAttendanceReward
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "String",
    "AppVersion" : "String",
    "MasterDataVersion" : "String",
}
```
* response
``` JSON
{
    "Result" : "ErrorCode",
}
```
