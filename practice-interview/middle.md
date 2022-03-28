# 프론트엔드 면접 준비

## 면접 중요도 (중)

### `typescript`에 대해서 알고 있는가? 사용해본적 있는지?

-> 타입스크립트는 자바스크립트의 슈퍼셋인 오픈소스 프로그래밍 언어이다.

- 쉬운말로 설명을 해보자면, 타입을 명시할 필요가 없는 인터프리터 언어인 비교적 유연한 자바스크립트와 달리, <b>정적 타입을 명시할 수 있다는 것이 순수한 자바스크립트와의 가장 큰 차이점</b>이다. 이로인한 장점이라 하면, 높은 개발 안정성과 편의성을 확보할 수 있다.
  그래서 대기업이나 큰 규모의 서비스를 제공하는 회사에서는 타입스크립트를 많이 사용한다. 나는 규모에 상관없이 미리 일어날 에러들에 대처 할수 있다는 것은 개발자에게도 많은 이점이 있고 생산성도 향상 될거라고 생각 되어서 관심을 가지게 되었다.
- 개발자가 의도한 변수나 함수 등의 목적을 더욱 명확하게 전달할 수 있고, 그렇게 전달된 정보를 기반으로 코드 자동 완성이나 잘못된 변수/함수 사용에 대한 에러 알림 같은 풍부한 피드백을 받을 수 있게 되므로 순수 자바스크립트에 비해 어마어마한 생산성 향상을 꾀할 수 있다. 즉, '자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것' 이 타입스크립트의 사용 목적이다.

[레퍼런스: 타입스크립트, 써야할까?](https://hyunseob.github.io/2018/08/12/do-you-need-to-use-ts/)

### 자바스크립트 테스팅

### `Event Loop`가 무엇이지?

### 프레임워크와 라이브러리의 차이?

### `URL` vs `URI`의 차이?

-> URI는 URL의 의미를 품고있다. <b>URL(Uniform Resource Locator)은 자원이 실제로 존재하는 위치</b>를 가리키며,URL은 흔히 웹 주소라고도 하며, 컴퓨터 네트워크 상에서 리소스가 어디 있는지 알려주기 위한 규약이다. URI의 서브셋이다. <b>URI(Uniform Resource Identifier)는 자원의 위치뿐만 아니라 자원에 대한 고유 식별자로서 URL을 의미를 포함</b>한다. URI는 특정 리소스를 식별하는 통합 자원 식별자(Uniform Resource Identifier)를 의미한다. 웹 기술에서 사용하는 논리적 또는 물리적 리소스를 식별하는 고유한 문자열 시퀀스다.
<u>URI는 식별하고, URL은 위치를 가르킨다.</u>
<br/>
<img src="https://www.charlezz.com/wordpress/wp-content/uploads/2021/02/www.charlezz.com-uri-url-uri-url-768x768.png">

Path Variable 방식과 Query Parameter 방식이 있다.

Path Variable 방식은 다음과 같다. 이는 어떤 특정한 자원을 보여줘야할때 사용된다.

```
/user/1
/user/2
/user/3
```

Query Parameter 방식은 다음과 같다. 이는 자원들을 필터링해서 보여줄때 사용된다.

```
/user?job=student
/user?job=student&age=10
```

[URI랑 URL 차이점이 뭔데?](https://www.charlezz.com/?p=44767)
[URL과 URI의 차이점](https://velog.io/@torang/URL%EA%B3%BC-URI%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
