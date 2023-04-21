# REST, REST API, RESTful

## REST 의미
* Representational State Transfer의 약자
* 자원을 URI로 구분하여 해당 자원의 상태(정보)를 주고 받거나 조작하는 것
* HTTP/HTTPS 프로토콜을 기반으로 클라이언트와 서버 사이의 통신에 사용되는 아키텍처 스타일
* HTTP를 그대로 사용하기에 웹의 장점을 살릴 수 있음

## REST 구성
* 자원(Resource)
    * URI : 모든 자원에 고유한 ID가 존재하고, 이 자원은 server에 존재함
    * HTTP의 route(경로)가 이에 해당함
* 행위(Verb)
    * 자원의 상태(정보)에 대한 요청 및 조작
    * HTTP의 Method가 이에 해당함
    * Create : 생성 (POST)
    * Read : 조회 (GET)
    * Update : 수정 (PUT)
    * Delete : 삭제 (DELETE)
* 표현(Representation of Resourc)
    * 클라이언트에게 보내는 데이터(응답 메시지의 body에 담김)
    * HTTP Response Message 헤더에 Content-Type으로 설정해줌 - JSON, XML, TEXT, RSS 등
    * JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이며, body에 content-type에 맞게 데이터를 보냄

## REST API
* REST의 규칙에 따라 서비스 API를 구현한 것
* 최근에는 OpenAPI가 REST API로 제공하는 추세
* HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 모든 환경에서 사용할 수 있음
* 다양한 클라이언트와 서버가 소통할 수 있고, 확장성과 재사용성을 높일 수 있음

## RESTful
* REST 원리를 따르는 시스템을 RESTful이라고 함
* REST API를 제공하는 웹서비스를 RESTful하다고 표현함
* RESTful은 REST를 REST답게 엄격하게 쓰기위한 방법을 의미하기도 함
* REST 방식이 공식적인 것은 아님. 법은 아니지만 사회적 규범이라고 보면 될듯

> 💡 위 내용 외에도 REST에 대해 구체적으로 알기 원하시면 아래 참고문헌의 [블로그]((https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html))를 참고해주세요

## 참고문헌
* [gmlwjd9405 블로그](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html) : 이 블로그 게시글 정독을 추천합니다.