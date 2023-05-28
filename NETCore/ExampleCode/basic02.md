# basic02

## 개관
> basic01과 같은 구조의 프로그램입니다. Program.cs와 LoginController.cs가 어떻게 생겼는지 basic01과 비교하면서 살펴봅시다.

## 요약
* LoginController
    * ControllerBase를 상속 받음
    * Login 하는 기능. ID, PW를 받고 Result를 반환함
    * URI {ServerIP:Port}/Login 으로 들어온 요청을 처리함
    * Post() 메소드는 Post요청에 대해 처리함