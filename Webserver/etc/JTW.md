# JWT(JSON Web Token)

## 의미
* 웹 및 모바일 어플리케이션에서 사용되는 인증 및 권한 부여를 위한 토큰 기반 인증 방식 중 하나
* SON 형태로 인코딩된 정보를 포함하고 있는 문자열로, 이를 사용하여 클라이언트 측에서 서버에게 자신의 신원을 증명하고 보안 권한을 얻을 수 있음
* URL-safe : base24url 인코딩 사용. URL로 이용할 수 있는 문자로만 구성됨
* [RFC7519 표준](https://www.rfc-editor.org/rfc/rfc7519)


## 사용 이유
* 웹 서버는 stateless 로 클라이언트와 요청을 주고 받기 때문에, 요청을 받았을 때 클라이언트가 누구인지 알 수 없음. 
* 매 요청마다 ID, PW를 주고 받을 수 없으니, 최초 접속시에만 ID,PW를 받아 인증을 하고 JWT를 발급하여 클라이언트한테 제공함.
* 이후 클라이언트는 요청할 때마다 JWT를 포함하여 데이터를 보내고, 서버는 JWT로 클라이언트를 특정하고 확인함.

## 구성
* Header : JWT 토큰의 유형과 해싱 알고리즘 등의 메타데이터를 포함
* payload : 토큰에 담을 클레임(claim) 정보를 포함. 이는 실제로 전송하려는 정보를 포함하며, 클라이언트 식별 정보, 만료시간 등이 포함됨. name-value의 한 쌍으로 이루어져 있으며, 여러개의 클레임을 넣을 수 있음
* signature : secret key를 포함하여 암호화 되어있음. 토큰이 유효한지 변조되지 않았는지 확인함

## 장점
* Stateless: 서버 쪽에서 상태를 유지하지 않기 때문에 서버 확장성이 높아짐
* Interoperability: JSON 형태로 전달되기 때문에 서로 다른 언어 및 플랫폼에서 사용 가능
* Extensibility: 클레임(claim)에 추가 정보를 포함시킬 수 있어서 사용자 다양한 정의 정보를 포함시킬 수 있음
* Security: JWT는 기본적으로 암호화되어 있어서 무단으로 데이터가 변경되거나 위조될 가능성이 적음
* REST 서비스로 제공 가능

## 단점 
* Payload Size: JWT는 정보를 Base64로 인코딩하여 전송하기 때문에 정보가 커지면 전송 시간과 용량에 대한 부담이 있을 수 있음
* Security: JWT가 안전하게 전달될 수 있도록 암호화되어 있지만, 암호화되지 않은 경우 해독될 가능성 있음. 클라이언트에 저장되기에 서버에서 사용자 정보를 조작해도 토큰에 직접 적용할 수 없음
* Revocation: JWT는 발급 후 만료 시간이나 권한 취소 등의 경우에도 서버에서 직접 처리해야 함. 즉, JWT를 강제로 만료시키는 것이 어려움
* statless 애플리케이션에서 토큰은 거의 모든 요청에 대해 전송되므로 데이터 트래픽 크기에 영향을 미칠 수음

## 참고
* JWS(JSON Web Signature) : JSON 데이터 구조를 사용하는 서명 표준[(RFC7515)](https://www.rfc-editor.org/rfc/rfc7515)
* JWE(JSON Web Encryption) : JSON 데이터 구조를 사용하는 암호화 방법[(RFC7516)](https://www.rfc-editor.org/rfc/rfc7516)

## 참고문헌
* [오픈나루](http://www.opennaru.com/opennaru-blog/jwt-json-web-token/)
* [위키피디아](https://ko.wikipedia.org/wiki/JSON_%EC%9B%B9_%ED%86%A0%ED%81%B0)