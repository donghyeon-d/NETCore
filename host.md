# WebApplication Host
## 의미
* WebApplication은 ASP.NET Core 6.0부터 추가된 새로운 호스트 빌더 API
* 앱 시작시 호스트를 빌드함 `var app = builder.Build();`
## 역할
* 아래와 같은 앱의 리소스를 캡슐화하여 갖고 있음
    * HTTP 서버 구현
    * Middleware components
    * Logging
    * Dependency injection (DI) services
    * Configuration
## Default Configuration
* Kestrel을 웹서버로 사용하고 IIS itegration을 사용하도록 설정함
*  appsettings.json, environment variables, command line arguments, properties/launchSettings.json 등을 통해 configuration을 구성함