# basic07

> 과제의 README에서는 "출력 필터를 사용하고 있다."라는 설명이 끝이다. 메모리에 값 저장하는 것과 출력필터 설정하는 것에 대한 내용입니다. 출력 필터는 이해가 잘 안되는 부분이 있기에, 추후 추가하려합니다.

## Program.cs
* 새롭게 보이는 코드가 크게 3가지가 있음
1. `builder.WebHost.ConfigureKestrel(options => options.ListenLocalhost(11500));`
    * 서버가 어느 포트로 listen할지 설정함. 11500 포트로 listen
    * [Properties > launchSettings.json]에서 applicationUrl의 포트를 변경해도 됨
2. `builder.Services.AddControllers().AddMvcOptions(options => options.Filters.Add(typeof(ResultFilterChangeResponse)));`
    * 결과 필터? 정확하게 모르겠음
    * (추후 내용 추가)
3. `builder.Services.AddMemoryCache();`
    * 애플리케이션에서 인메모리 캐시를 사용하도록 서비스 추가
    * LoginControll.cs 에서 private IMemoryCache MemoryCache 를 갖고 있음. 이때 사용할 서비스를 등록
    * 확인을 위해서 서버가 메모리상에 들고있어도 될만한 정보는 이를 통해 갖고 있어도 될듯
    * 예) 로그인시 앱버전, 마스터데이터 버전 등 확인
    * [매뉴얼](https://learn.microsoft.com/ko-kr/dotnet/api/microsoft.extensions.caching.memory.imemorycache?view=dotnet-plat-ext-7.0)