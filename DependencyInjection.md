# Dependency Injection (DI)

## 의미와 역할
* 객체 간의 의존성을 해결하는 디자인 패턴
* 객체 간의 의존성을 관리할 때 발생할 수 있는 복잡성과 중복 코드를 줄여서 유지보수성을 높일 수 있음
* 코드의 재사용성과 유지보수성을 향상시키며 객체 간의 결합도를 낮출 수 있음
* 인터페이스로 구현되어 있어서 의존성 주입을 쉽게할 수 있음
* 서비스(`builder.service`)로 의존성 주입을 구현하는데, 인터페이스와 구현체를 매핑하여 필요한 객체가 생성될 때(`bulder.build()`) 이를 생성하여 반환해줌
* 사용자 또는 프레임 워크가 제공하는 서비스를 추가할 수 있음
* ASP.NET Core 프레임 워크에서는 `builder.Add{GROUP_NAME}`으로 추가함

## 서비스 (Service)
* 애플리케이션의 특정 기능을 제공하기 위해 사용되는 클래스나 컴포넌트를 의미
* Service는 인터페이스와 해당 인터페이스를 구현하는 클래스의 두 가지 형태로 사용됨
* 사용 과정
    1. 서비스 컨테이너(인터페이스, 구현체) 구현 (ASP.NET Core에서 제공하는 것도 있음)
    2. 서비스 컨테이너로 객체의 인스턴스 생성
    3. 서비스 컨테이너에 등록 (builder.Service.Add{...})
    4. builder에 이 서비스 컨테이너 의존성 주입(DI)
* ASP.NET Core 예시 : DbContext, Logger, ...
* 서비스를 사용하여 의존성 주입함

## 사용 방법
3가지 방법으로 의존성 주입이 가능하고, 주입된 방식에 따라 수명주기가 달라짐. (자세한 설명은 MS Docs 참고)
1. [AddScoped](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addscoped?view=dotnet-plat-ext-5.0) : 지정된 형식의 범위 서비스 지정
2. [AddSingleton](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addsingleton?view=dotnet-plat-ext-5.0) : 싱글톤 서비스 지정
3. [AddTransient](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions.addtransient?source=recommendations&view=dotnet-plat-ext-7.0) : 임시서비스 지정
4. [확장 메소드 사용](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.dependencyinjection.servicecollection?view=dotnet-plat-ext-7.0)
* Add{GROUP_NAME}을 사용하여 관련 서비스 그룹을 등록할 수 있음.
* AddControllers 는 MVC 컨트롤러에 필요한 서비스를 등록함

## 코드 분석
* MVC 모델의 프로그램을 실행하는 프레임워크 예시
``` C#
// 1. 빌더 컨테이너 생성
var builder = WebApplication.CreateBuilder(args);

// 2. 빌더에 서비스를 추가함
// RazorPage 서비스 사용을 추가함
builder.Services.AddRazorPages();
// 컨트롤러와 뷰 서비스 사용을 추가함
builder.Services.AddControllersWithViews();

// 3. 위 서비스가 추가된 빌더 컨테이너로 어플리케이션 인스턴스를 만듦
var app = builder.Build();
```

## 참고문헌
* [MS Docs : dependency-injection](https://learn.microsoft.com/ko-kr/aspnet/core/fundamentals/dependency-injection?view=aspnetcore-7.0)
* [MS Docs : webapplicationbuilder](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.aspnetcore.builder.webapplicationbuilder?view=aspnetcore-7.0)
* [재우니의 블로그](https://aspdotnet.tistory.com/2761)
* [Gamechangers 블로그](https://gamechangers.tistory.com/142)