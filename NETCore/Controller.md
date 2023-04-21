# Controller

## 의미
* HTTP Request를 어떻게 처리해줄 것인지 정의함

## ControllerBase 클래스
* Controller가 요청을 받고 응답을 만들어주는 클래스
* 왠만한 것은 이 클래스 안에 다 들어있음 [(매뉴얼)](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.aspnetcore.mvc.controllerbase?view=aspnetcore-7.0)
* 내가 원하는 Controller를 만들어줄 때 이 클래스를 상속 받아서 내장된 기능을 활용하여 컨트롤러를 커스텀 해주면 됨
* 기능 : 상황별 응답생성(200, 300, 400 status code), 파일 반환, 모델 업데이트, 모델 유효성 검사
* Controller 클래스
    * ControllerBase를 상속받아 View의 기능을 추가한 클래스임
    * MVC model에서 사용하기 좋음
    * WebAPI 서버에서는 View의 기능은 필요 없으니 ControllerBase를 상속받아 사용하면 됨

## Attribute
### [ApiController] 
* 이 속성은 컨트롤러 클래스에 적용하여 HTTP API 응답을 제공하는 것과 관련된 동작을 할 수 있음
* 이 속성을 적용한 컨트롤러 클래스 이름에는 뒤에 `Controller` 를 붙이는 것이 관습 (예전 버전에서는 필수였음)
### 라우팅 `[Route("[controller]")]`
```C#
[ApiController]
[Route("[controller]")]
public class WeatherForecastController : ControllerBase
```

* [규칙기반 라우팅](https://learn.microsoft.com/ko-kr/aspnet/core/mvc/controllers/routing?view=aspnetcore-7.0#conventional-routing) 가능
* Route("...") 안에 [controller]를 쓰면, class 이름에서 Controller를 뺀 앞쪽의 단어를 그대로 적용하게 됨. "..."에 원하는 문자를 적어줄수도 있음
* 대/소문자를 구분하지 않음
* 계층적으로 구성해줄 수 있음. class를 Route로 감싸고, 액션을 또 라우트로 감싸면 계층적으로 설정됨
    
    ```C#
    [Route("Home")]
    public class HomeController : Controller
    {
        [Route("")]
        [Route("Index")]
        [Route("/")]
        public IActionResult Index()
        {
            return ControllerContext.MyDisplayRouteInfo();
        }

        [Route("About")]
        public IActionResult About()
        {
            return ControllerContext.MyDisplayRouteInfo();
        }
    }
    ```

* 요청 데이터(매개변수)가 어디에 담겨올지에 대한 정보
    * [Binding source parameter inference](https://learn.microsoft.com/en-us/aspnet/core/web-api/?view=aspnetcore-7.0#binding-source-parameter-inference)
    * Action 메소드의 매개변수 앞에 속성을 붙여줄 수 있음
    `[HttpPost]
public IActionResult Action3([FromBody] Product product, [FromBody] Order order)`

    |우선순위|Attribute|Binding source|
    |:---:|:---:|---|
    |1|[FromBody]|요청 본문. JSON 같은 복합 형식 정보|
    |2|[FromForm]|요청 본문에서의 form data|
    |3|[FromRoute]|요청 경로 데이터(URI)|
    |4|[FromQuery]|요청 쿼리 문자열 매개변수(URI?key=val)|
    |5|[FromHeader]|요청 헤더|
    |6|[FromServices]|작업 매개 변수로 삽입된 요청 서비스|
    |7|[AsParameters]|메서드 매개변수|
* [매뉴얼](https://learn.microsoft.com/ko-kr/aspnet/core/web-api/?view=aspnetcore-7.0#apicontroller-attribute)
### Http verb templates
* 동일한 route와 동일한 verb에 대해서는 한개의 컨트롤러 메소드만 지정해줄 수 있음
* [HttpGet] [HttpGet("{id}")]
    * GET 요청시 이 속성이 붙은 액션을 실행함
    * route/{id} 의 id값을 매개변수로 사용할 수 있음
* [HttpPost]
* [HttpPut]
* [HttpDelete]
* [HttpHead]
* [HttpPatch]
* 모든 템플릿은 route템플릿이며, 각 템플릿별로 속성을 갖고 있음(매뉴얼 참고)
* [매뉴얼](https://learn.microsoft.com/ko-kr/aspnet/core/tutorials/first-web-api?view=aspnetcore-7.0&tabs=visual-studio#routing-and-url-paths)
### [Consumes], [Produces]
* [Consumes](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.aspnetcore.mvc.consumesattribute?view=aspnetcore-7.0) : 받은 요청을 처리할 때 받은 데이터가 어떤 형식인지 지정함
    ``` C#
    [HttpPost]
    [Consumes("application/xml")]
    public IActionResult CreateProduct(Product product)
    ```
* [Produces](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.aspnetcore.mvc.producesattribute?view=aspnetcore-7.0) : 응답에 어떤 데이터 형식을 보낼지 지정함
    ``` C#
    [Produces(MediaTypeNames.Application.Json)]
    [Route("[controller]")]
    public class PetsController : MyControllerBase
    ```
### [[Bind]](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.aspnetcore.mvc.bindattribute?view=aspnetcore-7.0)
* 모델 바인딩에 포함할 접두사 및 속성을 지정함


## 참고 문헌
* [MS Docs](https://learn.microsoft.com/ko-kr/aspnet/core/web-api/?view=aspnetcore-7.0#apicontroller-attribute)
