# HTTP Message

## 의미
* HTTP는 웹상에서 보내는 어떤 규칙을 가진 문자열을 주고 받는데, 그 규칙이 HTTP를 의미함
* 그렇게 보내는 문자열을 HTTP Message라고 함
* 먼저 요청을 보내는 메시지를 Request 메시지, 요청에 대한 응답을 보내는 메시지를 Response 메시지라고 함

## Request Message (요청 메시지)
* 클라이언트가 서버로 보내는 메시지
* 형식
    ```plain text
    <메서드> <요청 URL> <버전>
    <헤더>

    <엔터티 본문>
    ```
    |분류|내용|
    |---:|:---|
    |시작줄|GET / HTTP/1.1|
    |헤더|Host: localhost:8000|
    | |Connection: keep-alive|
    | |(빈줄)| 
    |본문|body message|
    * 각 줄은 \r\n으로 구분되어있음
    * 위에 쓴 것 처럼 공백(띄어쓰기)도 유의해줘야 함
    * 헤더와 본문은 빈줄로 구분되어야 함
* 위 내용을 그냥 문자열로 만들어서 상태측에게 전달하는 것이 HTTP 요청 메시지
* `GET / HTTP/1.1\r\nHost: localhost:8000\r\nConnection: keep-alive\r\n\r\nbody message`

## Response Message (응답 메시지)
* 서버가 클라이언트에게 보내는 응답 메시지
* 형식
    ```plain text
    <버전> <상태코드> <사유구절>
    <헤더>

    <엔터티 본문>
    ```
    |분류|내용|
    |---:|:---|
    |시작줄|HTTP/1.1 200 OK|
    |헤더|Connection: keep-alive|
    | |Content-Type: text/html; charset=utf-8|
    | |Content-Length: 12|
    | |Set-Cokkie: name=donghyeon|
    | |(빈줄)| 
    |본문|body message|
    * 각 줄은 \r\n으로 구분되어있음
    * 위에 쓴 것 처럼 공백(띄어쓰기)도 유의해줘야 함
    * 헤더와 본문은 빈줄로 구분되어야 함
    * Content-Length와 본문 데이터의 길이가 동일해야 함
* 위 내용을 그냥 문자열로 만들어서 상태측에게 전달하는 것이 HTTP 응답 메시지
* `HTTP/1.1 200 OK\r\nConnection: keep-alive\r\nContent-Type: text/html; charset=utf-8\r\nContent-Length: 12\r\nSet-Cokkie: name=donghyeon\r\n\r\nbody message`

## Message Header
* 내가 보내는 메시지가 어떤 정보를 의미하는지에 대한 메타데이터
* 클라이언트 혹은 서버 프로그램은 헤더를 기준으로 요청 또는 응답을 처리하게 됨
* 꼭 필요하지 않은 정보가 포함될 수도 있지만, 어떤 정보는 없으면 응답하기 어려운 경우도 있음

## 참고문헌
* [HTTP 완벽가이드](http://www.yes24.com/Product/Goods/15381085)