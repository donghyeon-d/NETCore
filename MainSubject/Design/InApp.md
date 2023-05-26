# 인앱 결제 아이템 지급

## 기능
* 클라이언트가 스토어에서 인앱 결제 상품을 구매했고, 그 구매 영수증으로 아이템 지급을 요청함
* 서버는 중복 요청 검증을 하고 아이템을 지급함

## 로직 
* 구매 영수증을 클라이언트에게 받음
* 구매 영수증에 어떤 아이템이 포함되는지 등 정보를 가져옴(여기서는 임의로 만들었음)
* 구매 영수증을 mysql에 저장함. 이때 중복으로 인한 영수증 등록이 안될 경우 실패로 응답 반환함
* 구매 영수증에 따른 아이템을 클라이언트의 메일로 보냄

## 사용 DB
### Mysql
* GameDB.InAppPurchase
* GameDB.Mail

## API
> POST /InApp
* request
``` JSON
{
    "PlayerId" : "int",
    "AuthToken" : "string",
    "AppVersion" : "string",
    "MasterDataVersion" : "string",
    "ReceiptId" : "string"
}
```
* response
``` JSON
{
    "Result" : "ErrorCode"
}
```