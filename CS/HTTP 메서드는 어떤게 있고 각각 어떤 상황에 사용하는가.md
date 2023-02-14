# HTTP 메서드는 어떤게 있고 각각 어떤 상황에 사용하는가? (주요 메서드들만)

# GET

- 리소스 조회 메서드 (Read)
- 서버에 전달하고 싶은 데이터는 쿼리스트링을 통해서 전달
    - GET /members/100?username=woo
- 쿼리스트링 외에 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 서버에서 따로 구성해야 되기 때문에 지원하지 않는 곳이 많아서 권장하지 않음
- 조회할 때 POST도 사용할 수 있지만, GET 메서드는 캐싱이 가능하기에 GET을 사용하는것이 유리하다.

# POST

- 요청 데이터 처리, 주로 등록에 사용
- 전달한 데이터 처리/생성 요청 메서드 (Create)
- 메시지 바디 (body)를 통해 서버로 요청 데이터를 전달하면 서버는 요청 데이터를 처리하여 업데이트
- 전달된 데이터로 주로 신규 리소스 등록, 프로세스 처리에 사용
- 만일 데이터를 GET 하는데 있어, JSON으로 조회 데이터를 넘겨야 하는 애매한 경우 POST를 사용

# PUT

- 리소스를 대체(덮어쓰기), 해당 리소스가 없으면 생성
- 리소스를 대체(수정)하는 메서드 (Update)
- 만일 요청 메세지에 리소스가 있으면 덮어쓰고, 없으면 새로 생성한다.
    - /members/100 데이터가 존재하면 기존에 것을 완전 대체한다.
    - /members/100 데이터가 없으면 대체 할게 없으니까 새로 생성한다.
- 데이터를 대체해야 하니, 클라이언트가 리소스의 구체적인 전체 경로를 지정해 보내주어야 한다.
    - POST /members : 멤버 새로추가
    - PUT /members/100 : 100번째 멤버 수정

# PATCH

- 리소스를 부분 변경 (PUT이 전체 변경, PATCH는 일부 변경)
- 리소스 일부 부분을 변경하는 메소드 (Update)
- 만일 PATCH를 지원하지 않는 서버에서는 대신에 POST를 사용할 수 있다.

# DELETE

- 리소스 삭제
- 리소스를 제거하는 메서드 (Delete)
- 상태코드는 대부분 200을 사용하고 상황에 따라 204를 사용한다.

## 번외

### 204 코드 (No Content)

HTTP 204 No Content 성공 상태 응답 코드는 요청이 성공했으나 클라이언트가 현재 페이지에서 벗어나지 않아도 된다는 것을 나타냅니다.

흔히 204를 반환하는 경우는 [PUT](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/PUT) 요청에 대한 응답으로, 사용자에게 보여지는 페이지를 바꾸지 않고 리소스를 업데이트할 때 쓰입니다. 리소스를 생성한 경우엔 [201](https://developer.mozilla.org/ko/docs/Web/HTTP/Status/201) Created를 대신 반환합니다. 새롭게 업데이트한 페이지를 보여줘야 할 경우 [200](https://developer.mozilla.org/ko/docs/Web/HTTP/Status/200) 을 사용해야 합니다.

### 참고

[https://inpa.tistory.com/entry/WEB-🌐-HTTP-메서드-종류-통신-과정-💯-총정리](https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-HTTP-%EB%A9%94%EC%84%9C%EB%93%9C-%EC%A2%85%EB%A5%98-%ED%86%B5%EC%8B%A0-%EA%B3%BC%EC%A0%95-%F0%9F%92%AF-%EC%B4%9D%EC%A0%95%EB%A6%AC)

[https://developer.mozilla.org/ko/docs/Web/HTTP/Status/204](https://developer.mozilla.org/ko/docs/Web/HTTP/Status/204)