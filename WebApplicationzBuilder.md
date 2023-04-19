## WebApplicationzBuilder
### 구성
* 속성 : Configureation, Environment, Host, Logging, Services, WebHost
* 메소드 : Buile() - 설정된 내용을 기준으로 WebApplication 객체를 생성하여 리턴함
* 이 객체의 Service 속성에 의존성 주입함
### Service 속성
* 생성할 앱에 대한 서비스 컬렉션
* 사용자 또는 프레임 워크가 제공하는 서비스를 추가할 수 있음
* [IServiceCollection](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection?view=dotnet-plat-ext-7.0) 인터페이스로 생성되어 있음
### 확장 메소드 사용
* Add{GROUP_NAME}을 사용하여 관련 서비스 그룹을 등록할 수 있음.
* AddControllers 는 MVC 컨트롤러에 필요한 서비스를 등록함
### 사용예시 
* 로깅 서비스 사용 : builder.Services.AddLogging(); 
* 컨트롤러 사용 : builder.Services.AddControllers();
* Razorpage 사용 : builder.Services.AddRazorPages();
* 커스텀 서비스 사용 : builder.Services.AddScoped<IMyDependency, MyDependency>();
