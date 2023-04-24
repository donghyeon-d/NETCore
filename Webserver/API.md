# API(Application Programming Interface)

## 의미
* Application : 고유한 기능을 가진 모든 소프트웨어
* Interface : 두 애플리케이션 간의 서비스/통신 계약(규약). 요청과 응답을 사용하여 두 애플리케이션이 서로 통신하는 방법을 정의함
* API : 두 애플리케이션이 요청과 응답을 구성하는 방법에 대한 정보. 응용 프로그램에서 서비스를 호출하기 위한 인터페이스. 즉, API는 프로그램 간 상호작용을 위한 규칙, 규격, 프로토콜 등의 집합
* 두 애플리케이션은 API 라는 규칙으로 서로 요청을 하고 응답을 받음

## REST API
* REST방식을 적용한 API [(REST에 대한 자세한 내용은 게시글 참고)](./REST.md)
* WebAPI Server는 이 방식을 주로 사용함
* WebAPI와 REST API라는 용어는 서로 혼용해서 쓰고 있음

## API 유형
* Private API
    * 내부 API. 기업, 연구기관 등이 비즈니스 내에서 시스템과 데이터를 연결하는 데에 사용됨. 외부에 노출되지 않음
* Public API
    * 개방형 API로 기업, 연구기관 등의 외부에도 공개되어 외부 사람도 접근할 수 있음
    * 접근에 대한 권한 부여와 비용은 제공자의 정책에 따름
    * 접속하는 대상에 대한 제약이 없는 경우를 OpenAPI라고도 함
* Partner API
    * 특정 비즈니스 파트너 간의 데이터 공유
    * 특정인들만 사용할 수 있음

## 참고문헌
* [AWS](https://aws.amazon.com/ko/what-is/api/)
* [RadHat](https://www.redhat.com/ko/topics/api/what-are-application-programming-interfaces)
* [하늘네트](https://www.hanl.tech/blog/api%EB%9E%80-api%EC%9D%98-%EC%A0%95%EC%9D%98%EC%99%80-%EC%A2%85%EB%A5%98-%EC%9E%A5%EB%8B%A8%EC%A0%90/)