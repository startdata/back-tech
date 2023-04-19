# HTTP

## HTTP 프로토콜이란?

HTTP(Hypertext Transfer Protocol) 프로토콜이란 상호 간에 정의한 규칙을 의미하며 특정 기기 간에 데이터를 주고받기 위해 정의되었다.

웹에서는 브라우저와 서버 간에 데이터를 주고받기 위한 방식으로 HTTP 프로토콜을 사용하고 있다.

## HTTP 프로토콜 특징

HTTP 프로토콜은 상태가 없는(stateless) 프로토콜이다. 여기서 상태가 없다라는 말은 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리가 된다는 말이다. 이전 데이터 요청과 다음 데이터 요청이 서로 관련이 없다.

이러한 특징 덕택에 서버는 세션과 같은 별도의 추가 정보를 관리하지 않아도 되고, 다수의 요청 처리 및 서버의 부하를 줄일 수 있는 성능 상의 이점이 생긴다..

HTTP 프로토콜은 일반적으로 TCP/IP 통신 위에서 동작하며 기본 포트는 80번

## HTTP Request & HTTP Response

HTTP 프로토콜로 데이터를 주고받기 위해서는 아래와 같이 요청(Request)을 보내고 응답(Response)을 받아야 한다.

![https://joshua1988.github.io/images/posts/web/http/request-response.png](https://joshua1988.github.io/images/posts/web/http/request-response.png)

클라이언트란 요청을 보내는 쪽을 의미하며 일반적으로 웹 관점에서는 브라우저를 의미합니다. 서버란 요청을 받는 쪽을 의미하며 일반적으로 데이터를 보내주는 원격지의 컴퓨터를 의미합니다.

## URL

URL(Uniform Resource Locators)

![https://joshua1988.github.io/images/posts/web/http/url-structure.png](https://joshua1988.github.io/images/posts/web/http/url-structure.png)

## HTTP 요청 메서드

앞에서 살펴본 URL을 이용하면 서버에 특정 데이터를 요청할 수 있습니다. 여기서 요청하는 데이터에 특정 동작을 수행하고 싶으면 어떻게 해야 할까요? 바로 HTTP 요청 메서드(Http Request Methods)를 이용합니다.

일반적으로 HTTP 요청 메서드는 HTTP Verbs라고도 불리우며 아래와 같이 주요 메서드를 갖고 있습니다.

- **GET** : 존재하는 자원에 대한 **요청**
- **POST** : 새로운 자원을 **생성**
- **PUT** : 존재하는 자원에 대한 **변경**
- **DELETE** : 존재하는 자원에 대한 **삭제**

이와 같이 데이터에 대한 조회, 생성, 변경, 삭제 동작을 HTTP 요청 메서드로 정의할 수 있습니다. 참고로 때에 따라서는 POST 메서드로 PUT, DELETE의 동작도 수행할 수 있습니다.

기타 요청 메서드는 다음과 같습니다.

- HEAD : 서버 헤더 정보를 획득. GET과 비슷하나 Response Body를 반환하지 않음
- OPTIONS : 서버 옵션들을 확인하기 위한 요청. [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)에서 사용

## HTTP 상태 코드

앞에서 살펴본 URL과 요청 메서드가 클라이언트에서 설정해야 할 정보라면 HTTP 상태 코드(HTTP Status Code)는 서버에서 설정해주는 응답(Response) 정보입니다

### 2xx - 성공

200번대의 상태 코드는 대부분 성공을 의미합니다.

- 200 : GET 요청에 대한 성공
- 204 : No Content. 성공했으나 응답 본문에 데이터가 없음
- 205 : Reset Content. 성공했으나 클라이언트의 화면을 새로 고침하도록 권고
- 206 : Partial Conent. 성공했으나 일부 범위의 데이터만 반환

### 3xx - 리다이렉션

300번대의 상태 코드는 대부분 클라이언트가 이전 주소로 데이터를 요청하여 서버에서 새 URL로 리다이렉트를 유도하는 경우입니다.

- 301 : Moved Permanently, 요청한 자원이 새 URL에 존재
- 303 : See Other, 요청한 자원이 임시 주소에 존재
- 304 : Not Modified, 요청한 자원이 변경되지 않았으므로 클라이언트에서 캐싱된 자원을 사용하도록 권고. [ETag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag)와 같은 정보를 활용하여 변경 여부를 확인

### 4xx - 클라이언트 에러

400번대 상태 코드는 대부분 클라이언트의 코드가 잘못된 경우입니다. 유효하지 않은 자원을 요청했거나 요청이나 권한이 잘못된 경우 발생합니다. 가장 익숙한 상태 코드는 404 코드입니다. 요청한 자원이 서버에 없다는 의미죠.

- 400 : Bad Request, 잘못된 요청
- 401 : Unauthorized, 권한 없이 요청. Authorization 헤더가 잘못된 경우
- 403 : Forbidden, 서버에서 해당 자원에 대해 접근 금지
- 405 : Method Not Allowed, 허용되지 않은 요청 메서드
- 409 : Conflict, 최신 자원이 아닌데 업데이트하는 경우. ex) 파일 업로드 시 버전 충돌

### 5xx - 서버 에러

500번대 상태 코드는 서버 쪽에서 오류가 난 경우입니다.

- 501 : Not Implemented, 요청한 동작에 대해 서버가 수행할 수 없는 경우
- 503 : Service Unavailable, 서버가 과부하 또는 유지 보수로 내려간 경우

# Header

헤더는 크게 4가지로 분류할 수 있다.

- General Header(공통 헤더)
- Request Header(요청 헤더)
- Response Header(응답 헤더)
- Entity Header(엔티티 헤더)

### General Header(공통 헤더)

요청과 응답 모두에 적용되지만 바디에서 최종적으로 전송되는 데이터와는 관련이 없는 헤더

- [Date](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Date) : 현재시간
- [Pragma](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Pragma) : 캐시제어 , HTTP/1.0에서 쓰던 것으로 HTTP/1.1에서는 Cache-Control이 쓰인다.
- [Cache-Control](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cache-Control) : 캐시를 제어할 때 사용
- [Upgrade](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Upgrade) : 프로토콜 변경시 사용
- [Via](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Via) : 중계(프록시)서버의 이름, 버전, 호스트명
- [Connection](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Connection) : 네트워크 접속을 유지할지 말지 제어. HTTP/1.1은 kepp-alive 로 연결 유지하는게 default 값
- [Transfer-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Transfer-Encoding) : 사용자에게 entity를 안전하게 전송하기 위해 사용하는 인코딩 형식을 지정

### Entity Header(엔티티 헤더)

컨텐츠 길이나 MIME 타입과 같이 엔티티 바디에 대한 자세한 정보를 포함하는 헤더

- [Content-type](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Type) : 리소스의 media type 명시 ex) application/json, text/html
- [Content-Length](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Length) : 바이트 단위를 가지는 개체 본문의 크기
- [Content-language](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Language) : 본문을 이해하는데 가장 적절한 언어
- [Content-location](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Location) : 반환된 데이터 개체의 실제 위치 ex) /index.html
- [Content-disposition](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Disposition) : 응답 메세지를 브라우저가 어떻게 처리할지. 주로 다운로드에 사용
- [Content-Security-Policy](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Security-Policy) : 다른 외부 파일을 불러오는 경우 차단할 리소스와 불러올 리소스 명시
  - ex) default-src https -> https로만 파일을 가져옴
  - ex) default-src 'self' -> 자기 도메인에서만 가져옴
  - ex) default-src 'none' -> 외부파일은 가져올 수 없음
- [Content-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Encoding) : 본문의 리소스 압축 방식. 주로 Content-Type과 같이 사용되며 참조되는 미디어 타입을 얻도록 디코드하는 방법을 클라이언트가 알게 해줍니다.
- [Location](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Location) : 301, 302 상태코드일 때만 볼 수 있는 헤더로 서버의 응답이 다른 곳에 있다고 알려주면서 해당 위치(URI)를 지정
- [Last-Modified](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Last-Modified) : 리소스의 마지막 수정 날짜
- [Allow](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Allow) : 지원되는 HTTP 요청 메소드 ex) GET, HEAD, POST
- [Expires](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers) : 자원의 만료 일자
- [ETag](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/ETag) : 리소스의 버전을 식별하는 고유한 문자열 검사기(주로 캐시 확인용으로 사용)

### Request Header(요청 헤더)

HTTP 요청에서 사용되지만 메시지의 컨텐츠와 관련이 없는 패치될 리소스나 클라이언트 자체에 대한 자세한 정보를 포함하는 헤더

- [Host](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Host) : 요청하려는 서버 호스트 이름과 포트번호
- [User-agent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) : 클라이언트 프로그램 정보 ex) Mozilla/4.0, Windows NT5.1
- [Referer](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Referer) : 현재 페이지로 연결되는 링크가 있던 이전 웹 페이지의 주소
- [Accept](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept) : 클라이언트가 처리 가능한 MIME Type 종류 나열
- [Accept-charset](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept-Charset) : 클라이언트가 지원가능한 문자열 인코딩 방식
- [Accept-language](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept-Language) : 클라이언트가 지원가능한 언어 나열
- [Accept-encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Accept-Encoding) : 클라이언트가 해석가능한 압축 방식 지정
- [If-Modified-Since](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/If-Modified-Since) : 여기에 쓰여진 시간 이후로 변경된 리소스 취득. 캐시가 만료되었을 때에만 데이터를 전송하는데 사용
- [Authorization](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Authorization) : 인증 토큰을 서버로 보낼 때 쓰이는 헤더
- [Origin](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Origin) : 서버로 Post 요청을 보낼 때 요청이 어느 주소에서 시작되었는지 나타내는 값. 경로 정보는 포함하지 않고 서버 이름만 포함
  - 이 값으로 요청을 보낸 주소와 받는 주소가 다르면 CORS 에러가 난다.
- [Cookie](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Cookie) : 쿠기 값 key-value로 표현된다. Set-Cookie 헤더와 함께 서버로부터 이전에 전송됐던 저장된 HTTP 쿠키를 포함

### Response Header(응답 헤더)

위치 또는 서버 자체에 대한 정보(이름, 버전)과 같이 응답에 대한 부가적인 정보를 갖는 헤더

- [Server](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Server) : 웹서버의 종류
- [Age](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Age) : max-age 시간내에서 얼마나 흘렀는지 초 단위로 알려주는 값
- [Referrer-policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referrer-Policy) : 서버 referrer 정책을 알려주는 값 ex) origin, no-referrer, unsafe-url
- [WWW-Authenticate](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/WWW-Authenticate) : 사용자 인증이 필요한 자원을 요구할 시, 서버가 제공하는 인증 방식
- [Proxy-Authenticate](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authenticate) : 요청한 서버가 프록시 서버인 경우 유저 인증을 위한 값
- [Set-Cookie](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Set-Cookie) : 서버측에서 클라이언트에게 세션 쿠키 정보를 설정 (RFC 2965에서 규정)
