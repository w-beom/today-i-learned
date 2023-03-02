# HTTP 요청 헤더에는 어떤게 들어가는가?

- Accept : 클라이언트가 처치 가능한 MIME Type 종류 나열
- Accept-Encoding : 클라이언트가 해석가능한 압축 방식 지정
- Accept-Language : 클라이언트가 지원가능한 언어 나열
- Connection : 네트워크 접속을 유지할지 말지 제어. HTTP/1.1은 keep-alive로 연결 유지하는게 default 값
- Content-Length : 바이트 단위를 가지는 개체 본문의 크기
- Content-type : 리소스의 midea type 명시 ex) application/json, text/html
- Cookie : 쿠키 값 key-value로 표현된다. Set-Cookie 헤더와 함께 서버로부터 이전에 저장된 HTTP 쿠키를 포함
- Host : 요청하려는 서버 호스트 이름과 포트번호
- Origin : 서버로 Post 요청을 보낼 때 요청이 어느 주소에서 시작되었는지 나타내는 값. 경로 정보는 포함하지 않고 서버 이름만 포함
    - 이 값으로 요청을 보낸 주소와 받는 주소가 다르면 CORS에러가 난다.
- Pragma : 캐시제어 HTTP/1.0에서 쓰던 것으로 HTTP/1.1 에서는 Cacche-Control이 쓰인다.
- Referer : 현재 페이지로 연결되는 링크가 있던 이전 웹 페이지의 주소
- User-Agent : 클라이언트 프로그램 정보 ex) Mozilla/4.0, Windows NT5.1

## CORS 에러는 어디서 나는건가?

CORS 에러는 클라이언트에서 다른 도메인의 서버로 요청을 보낼 때 발생할 수 있다. 서로 다른 도메인에서 요청을 보내는 것은 보안상 위험할 수 있기 때문에 브라우저에서는 보안 정책을 강제한다. 따라서, 서버에서 CORS 정책을 설정하지 않은 경우 클라이언트에서 요청한 리소스를 사용할 수 없어 에러가 발생한다.

Origin 헤더를 포함해서 CORS 이슈를 해결하려면 서버에서 CORS 정책을 설정해야 한다. 서버는 Access-Control-Allow-Origin 헤더를 설정하여 요청을 보낸 도메인을 허용할 수 있다. 또한, 서버에서는 요청에 대한 응답으로 Access-Control-Allow-Headers, Access-Control-Allow-Methods 등의 헤더를 설정할 수 있다.

## Origin 헤더를 포함해서 CORS 이슈를 해결하려면 어떻게 해야하는가?

서버에서는 Access-Control-Allow-Origin 헤더를 설정하여 요청을 보낸 도메인을 허용할 수 있다. 이 헤더를 설정할 때, 모든 도메인을 허용하는 "*" 와 특정 도메인만을 허용하는 방법이 있다. 또한, 서버에서는 요청에 대한 응답으로 Access-Control-Allow-Headers, Access-Control-Allow-Methods 등의 헤더를 설정할 수 있다. 이를 통해 서버에서는 CORS 정책을 설정해 클라이언트에서 요청한 리소스를 사용할 수 있게 된다.
