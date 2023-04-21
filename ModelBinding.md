# Model Binding

## 의미
* 모델(data)를 연결시키는 것
* 클라의 요청을 처리하기 위해서는 서버가 필연적으로 데이터를 다룰 수밖에 없음. 이 데이터(모델)들을 서버에서 어떻게 접근할지 설정하는 것

## 데이터 종류
### 1. Binding Model
* 클라이언트에서 보낸 Request를 파싱하기 위한 데이터 모델
* 유효성 검증이 필수
### 2. Application Model
* 서버의 각종 서비스들이 사용하는 데이터 모델
* 예) class WeatherForecast (WeatherForecast.cs)
### 3. View Model
* Model - View - Controller 사이에서 View에게 넘겨주기 위한 데이터 모델
* UI를 만들기 위한 데이터 모델
### 4. API Model
* WebAPI Controller 에서 사용하는 데이터 모델
* JSON, XML 등의 포맷으로 응답할 때 필요한 데이터 모델

## Binding Model 종류
### 1. Form Values
* Request의 Body에서 보낸 값
* HTTP POST 요청에서 body에 들어온 값을 의미함

### 2. Routes Values
* routing할 때 URL 매칭이나 Default Value에 의해 적용되는 값

### 3. Query string Values
* URL 끝에 붙이는 방법
* ? 뒤에 붙고, http url 규약에 따름
* HTTP GET 요청에서 이 방식을 따름
* www.url.com/?Name=dongchoi&id=123
* 대문자/소문자 구분하지 않음. 같은 값으로 봄

### * 우선순위
* 위의 1,2,3 순서대로 우선순위를 가짐
* 헷갈릴 수 있으니, 가능한 한가지 종류를 사용하는 것이 좋을 듯

> WebAPI 서버에서는 클라가 서버로 값을 보낼 땐 POST요청 + Form Values으로 보내는 경우가 많음. 클라가 값을 받는 GET 요청할 땐 Routes Values or Query string Values를 함

## Complex Types
* 넘겨받을 인자가 너무 많아지면 부담스러워지니까, 별도의 **모델링 클래스**를 만들어주는 것
(함수가 받는 인자가 너무 많으면 안좋으니까, 구조체로 묶어주는 느낌)
* 새로운 모델링 클래스를 만들었으면, 메소드의 인자에 그냥 넣어주기만 하면 됨. ASP.NET에서 알아서 처리됨