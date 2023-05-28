# basic01

## 개관
> ASP.NET Core Web API 기본 템플릿으로 만든 프로그램입니다.
> program.cs의 구조와 Controller, router에 대해서 이해해봅시다.

## Program.cs
``` C#
// 미리 구성된 기본값을 사용하여 WebApplication의 인스턴스 builder를 생성함
var builder = WebApplication.CreateBuilder(args);

// 컨트롤러 서비스를 미들웨어에 등록함
builder.Services.AddControllers();

// builder로 application을 만듦
var app = builder.Build();

// Develop 버전이 아니면, 예외 페이지 사용을 추가함
if (!app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}

// Routing 서비스 사용 추가
app.UseRouting();

// Endpoint 서비스 사용 추가
app.UseEndpoints(endpoints => { endpoints.MapControllers(); });

// 앱 실행
app.Run();
```

## WeatherForecastController.cs
1. ApiController 임을 명시

    `[ApiController]` 속성 사용

2. Route 경로 지정

    `[Route("[controller]")]`
    * `public class WeatherForecastController`의 Controller 접미사를 뺀 WeatherForecast가 경로가 됨
    * URI : {serverIP:port}/WeatherForecast

3. Http verb 지정
    ```C#
    [HttpGet]
    public IEnumerable<WeatherForecast> Get()
    {
        var rng = new Random();
        return Enumerable.Range(1, 5).Select(index => new WeatherForecast
        {
            Date = DateTime.Now.AddDays(index),
            TemperatureC = rng.Next(-20, 55),
            Summary = Summaries[rng.Next(Summaries.Length)]
        })
        .ToArray();
    }
    ```
    * GET 요청을 받았을 때, 이 메소드를 실행함
    * 이 메소드의 return value가 Http response의 body data에 JSON형식으로 들어감
4. 기타
    * logger는 basic04에서 자세히 보도록 하자