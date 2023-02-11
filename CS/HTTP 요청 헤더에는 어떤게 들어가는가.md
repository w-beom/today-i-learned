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
