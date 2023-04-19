# Program.cs

## 의미와 역할
* 어플리케이션 시작 코드가 써있는 파일
* C/C++에서의 main 함수 파일 역할을 함
* 앱에서 요구하는 서비스를 설정함
* 앱의 요청을 핸들링할 수 있게 미들웨어들을 구성하고 파이프라이닝 함

<br>

---

<br>

## 구성
* 프로그램 시작옵션 및 DI 서비스를 지정하는 것을 Startup.cs 파일에서 했으나, 현재는 program.cs 파일로 통합됨
* main 클래스를 만들어 실행 메소드를 만들어서 실행했지만, [최상위 문(Top-level statements)](https://learn.microsoft.com/ko-kr/dotnet/csharp/fundamentals/program-structure/top-level-statements)으로도 사용할 수 있음. VS 2022 기준으로 프로젝스 생성시 최상위 문 세팅이 디폴트로 설정돼있음 (C# 9 부터)

<br>

---

<br>

## 코드 분석
기본적인 흐름은 다음과 같음
1. using namespace
2. builder의 인스턴스를 만듦 (class WebApplicationBuilder)
3. 종속성 주입(Dependency Injection) : 빌더 인스턴스에 서비스를 등록함 (컨트롤러 등)
4. 빌더로 앱의 객체를 만듦 (class WebApplication)
5. 미들웨어 설정 : 앱에서 사용하고자 하는 것들을 지정함
6. 앱을 실행함

```C#
// 1. using namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

// 2. builder의 인스턴스를 만듦 : 미리 구성된 기본값을 사용하여 WebApplication의 인스턴스 builder를 생성함
var builder = WebApplication.CreateBuilder(args);

// 3. 종속성 주입(Dependency Injection)
// Add services to the container. 
builder.Services.AddControllers();
// 필요시 서비스를 빌더 컨테이너에 더 추가할 수 있음

// 4. 빌더로 앱의 객체를 만듦
var app = builder.Build();

// 5. 미들웨어 설정
// Configure the HTTP request pipeline.
// Devleop 버전이 아닐 때 Exception page를 사용함
if (!app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}

// Routing을 사용함
app.UseRouting();

// Endpoint 지정
app.UseEndpoints(endpoints => { endpoints.MapControllers(); });

// 6. 앱을 실행함
// 설정이 다 끝났으면 앱을 실행함
app.Run();
```

