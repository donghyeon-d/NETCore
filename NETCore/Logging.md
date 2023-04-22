# Logging

## 의미와 역할
* 애플리케이션의 동작 중에 필요한 상황에 필요한 내용을 출력(기록)하는 것
* 로그 수준을 나눠서 중요도에 따라 관리할 수 있음
* 비동기를 지원하지 않음(매우 빨라서 굳이 비동기로 할 필요 없음)
    * 느린 데이터 저장소에 저장하고 싶다면, 메시지 큐를 통해 로깅하는 방법이 따로 있음 [(참고)](https://github.com/dotnet/AspNetCore.Docs/issues/11801)


## 로그 사용
* WebApplicationBuilder안에 있는 _hostApplicationBuilder 안에 있는 LoggingBuilder가 Logging이라는 property를 만들어서 뱉어줌. -> 그냥 builder.Logging으로 접근할 수 있음
* Logger 생성 및 설정
    ``` C#
    // program.cs
    // builder 생성
    var builder = WebApplication.CreateBuilder(args);
    // Logging 안에 있는 내용물 초기화(설정돼 있는 공급자 초기화)
    builder.Logging.ClearProviders();
    // Logging 공급자 추가 Add{provider} 이 코드 경우 Console이라는 공급자
    builder.Logging.AddConsole();
    ```
* Logging 하기
    ``` C#
    // 원하는 로직 위치에서 Log-level에 맞는 메소드 호출
    Logger.Log{LogLevel}("Logging Message ... ");
    ```

## 로그 공급자 Logging providers
* Logging Provider에는 Console, Debug, EventSource, EventLog가 있으며, Third-party로 NuGet에서 패키지를 받을 수 있음
* 내가 원하는 특정 파일에 로깅을 하고 싶으면, third-party provider를 사용해야 함

## Log-level
* 중요한 정도 혹은 위험한 정도에 따라 Log-level을 구분해놓았음. 상황에 맞는 수준의 메서드를 사용하여 로깅하면 됨
* 숫자가 높을 수록 Log-level이 높다고 할 수 있음
    |LogLevel|값|메서드|설명|
    |---|---|---|---|
    |Trace|0|LogTrace|가장 자세한 메시지를 포함. 해당 메시지는 중요한 앱 데이터를 포함할 수 있음|
    |Debug|1|LogDebug|디버깅 및 개발을 위한 수준|
    |Information|2|LogInformation|앱의 일반적인 흐름을 추적. 장기적인 값이 있음|
    |Warning|3|LogWarning|비정상적이거나 예기치 않은 이벤트를 위한 수준. 일반적으로 앱의 오류를 발생시키지 않는 오류 또는 조건을 포함|
    |Error|4|LogError|처리할 수 없는 오류 및 예외를 위한 수준. 해당 메시지는 전체 앱 오류가 아닌 현재 작업 또는 요청의 오류|
    |Critical|5|LogCritical|즉각적인 대응이 필요한 오류를 위한 수준. 예) 데이터 손실 시나리오, 디스크 공간 부족|
    |None|6||로깅 범주에서 메시지를 쓰지 않도록 지정함|

## config setting
* `appsettings.json`에서 필요에 따라 Logging에 대한 설정을 해줄 수 있음. 공급자에따라 로그 레벨 등을 지정해줄 수 있음
* 설정한 로그 레벨보다 수준이 높은 Log가 logging됨
* 다음은 `appsettings.json` 예시 파일
    ``` JSON
    {
        // Logging 설정은 "Logging"범주 안에 있어야 함
        "Logging": {
            "LogLevel": { // 모든 공급자에게 기본적으로 적용하는 값
            "Default": "Error", // Default logging, Error and higher.
            "Microsoft": "Warning" // All Microsoft* categories(namespace), Warning and higher.
            },
            "Debug": { // Debug provider는 이 규칙에 따름 (위의 Logvel의 값을 덮어씀)
            "LogLevel": {
                "Default": "Information", // Overrides preceding LogLevel:Default setting.
                "Microsoft.Hosting": "Trace" // Debug:Microsoft.Hosting category.
            }
            },
            "EventSource": { // EventSource provider는 이 규칙에 따름 (위의 Logvel의 값을 덮어씀)
            "LogLevel": {
                "Default": "Warning" // All categories of EventSource provider.
            }
            }
        }
    }   
    ```


## 참고문헌
* [MS Docs](https://learn.microsoft.com/ko-kr/aspnet/core/fundamentals/logging/?view=aspnetcore-7.0)