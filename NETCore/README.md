# Intro

> 컴투스 서버캠퍼스 1기의 첫번째 과제를 수행하면서 만든 문서입니다. 이번 파트는 ASP.NET Core 에 대해서 학습합니다. [WebServer 파트](./Webserver/README.md)의 학습을 통해 웹서버에 대한 배경 지식을 먼저 살펴보시는 것을 추천합니다.<br>

> ASP.NET Core는 MS에서 만들 C#언어 기반의 웹 프레임워크입니다. 웹 프론트와 서버 모두 구현할 수 있는 서비스를 제공합니다. 한때는 Windows에서만 개발 가능했지만, 지금은 일부 기능을 제외하고는 Linux와 MacOS에서도 개발할 수 있게 제공되고 있습니다.

## Program.cs
main 함수 파일 역할을 하며 애플리케이션을 세팅하고 실행함

## Dependency Injection (DI)
객체 간의 의존성을 해결하는 디자인 패턴. 프레임워크의 동작 내부에서 어떤 서비스 객체가 생성/사용/소멸이 잘 될 수 있게 기능함

## WebApplication Host
앱의 리소스를 캡슐화하여 갖고 있음

## MVC
데이터(Model) - 사용자 인터페이스(View) - 논리제어(Controller) 로 나눈 소프트웨어 디자인 패턴. WebAPI Server에서는 여기서 View만 빠진 형태

## Middleware
양 쪽을 연결하여 데이터를 주고 받을 수 있도록 중간에서 매개 역할을 하는 소프트웨어

## Model Binding
모델(data)를 연결시키는 작업

## Controller
요청을 받고 응답을 만들어주는 역할을 함

## Configure
애플리케이션에서 사용하는 환경변수 모음

## Logging
애플리케이션의 동작 중에 필요한 상황에 필요한 내용을 출력(기록)하는 것

## Library
ASP.NET Core의 기본 라이브러리에 대한 소개

## 안내사항
학습하면서 작성한 문서이기에 잘못된 내용이 있을 수 있습니다. 수정이 필요한 부분이 있으면 `ehdgus6634@naver.com` 으로 메일을 보내주시면 확인하겠습니다.