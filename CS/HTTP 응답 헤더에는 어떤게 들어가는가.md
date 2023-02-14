# HTTP 응답 헤더에는 어떤게 들어가는가?

- Server : 웹 서버의 정보를 명시 ex ) Apache/2.2.24
- Location : 응답 코드 301, 302 리다이렉션 상태에서 위치 정보를 지정
- Content-Encoding : 데이터의 압축 방식을 지정
- Content-type : 리소스의 midea type 명시 ex) application/json, text/html
- Cache-control : Cache 속성을 설정
    - no-store : 캐시를 저장하지 않음
    - no-cache : 서버에 확인 후 캐시 사용
    - must - revalidate : 만료된 캐시를 서버에 확인
    - public : 공유 캐시에 저장
    - private : 특정 사용자 환경에만 저장
    - max-age : 캐시 유효 기간 명시
- Set-Cookie : 클라이언트에 저장할 쿠키 정보를 지정
    - Expires : 만료일
    - Secure : HTTPS에서만 사용
    - HttpOnly : 스크립트에서 접근 불가
    - Domain : 같은 도메인에서만 사용
- Expires : 해당 리소스의 유효 일시를 지정
- Allow : 응답 코드 405 (Method Not Allowed) 상태에서 서버가 제공할 수 있는 HTTP 메서드를 지정