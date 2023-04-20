# URL과 Resource

## URL(Uniform Resource Locator)이란?
* 인터넷의 리소스를 가리키는 표준 이름(주소)
* 전자정보 일부를 가리키고 그것이 어디에 있고 어떻게 접근할 수 있는지 알려줌
* 리소스가 있는 위치, 경로, 요구사항, 부가정보 등이 합쳐진 문장

## URL 문법
`<스킴>://<호스트>:<포트>/<경로>;<파라미터>?<질의>#<프래그먼트>`
* 스킴(scheme) : 주어진 리소스에 어떻게(어떤 프로토콜로) 접근할지에 대한 정의 (http or https)
* 호스트(host) : 접근하려는 서버의 도메인 주소(IP address)
* 포트(port) : 호스트의 포트 번호
    * 웹 브라우저는 입력된 스킴에 따라 포트 번호를 알아서 부여하여 요청함
    * http는 80 port, https는 443 port
* 경로(route) : 호스트의 포트로 갔을 때, 리소스가 어디에 있는지에 대한 정보
    * 서버에서 routing을 한다고 하면, 이 값을 보고 이 값에 따른 동작을 해주는 것
    * 계층적 파일 시스템 경로와 유사한 구조를 가짐
* 파라미터(parameter) : 정확한 요청을 위해서 파라미터를 전달하기 위해 사용함
    * 앞의 내용과는 ';'으로 구분하며, key=value로 전달함. 여러개의 쌍을 보낼 수 있음
    * 질의(query) 문자열과 비슷하게 사용하고, 
* 질의(query) : 데이터베이스 같은 서비스들은 요청받을 리소스 형식의 범위를 좁히기 위한 추가 정보를 포함
    * ‘?’  뒤에 나오며, ‘이름=값’ 쌍 형식의 질의 문자열을 요구함. 쌍을 구분하기 위해서는 ‘&’를 사용함
* 프래그먼트(fragment) : 리소스를 여러개의 조각으로 나눠져있을 수 있는데, 그 조각을 가리키기 위한 요소
    * ‘#’ 뒤에 나옴

* 예시) `https://www.example.com:8080/path/to/resource;param1=value1?query=string#fragment`
    * 스킴: https
    * 호스트: www.example.com
    * 포트: 8080
    * 경로: /path/to/resource
    * 파라미터: param1=value1
    * 질의: query=string
    * 프래그먼트: fragment

## 참고문헌
* [HTTP 완벽가이드](http://www.yes24.com/Product/Goods/15381085)
