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

### `API`와 `Endpoint`의 차이?

#### API란?

= API는 프로그램 혹은 시스템 간의 통신하는 창구, 즉 프로그램들이 서로 상호작용하는 것을 도와주는 매개체라 할 수 있다.

1. <b>API는 서버와 데이터베이스에 대한 출입구 역할을 한다.</b>

   - 데이터베이스에는 소중한 정보들이 저장된다. 그렇기에 모든 사람들이 이 데이터베이스에 접근할 수 있어서는 안된다. API는 이를 방지하기 위해 사람들이 가진 서버와 데이터베이스에 대한 출입구 역할을 하며, 허용된 사람들에게만 접근성을 부여해준다.

2. <b>API는 애플리케이션과 기기가 원활하게 통신할 수 있도록 한다.</b>

   - 여기서 애플리케이션이란 우리가 흔히 알고 있는 스마트폰 어플이나 프로그램을 말한다.
     API는 애플리케이션과 기기가 데이터를 원활히 주고받을 수 있도록 돕는 역할을 한다.

3. <b>API는 모든 접속을 표준화한다.</b>
   - API는 모든 접속을 표준화하기 때문에 기계/ 운영체제 등과 상관없이 누구나 동일한 액세스를 얻을 수 있다. 쉽게 말해, API는 범용 플러그처럼 작동한다고 볼 수 있겠다.

#### Endpoint?

= 엔드포인트는 서비스를 사용가능하도록 하는 서비스에서 제공하는 커뮤니케이션 채널의 한쪽 끝.
즉 요청을 받아 응답을 제공하는 서비스를 사용할 수 있는 지점을 의미 한다.

예를 들어 지하철 최단 거리 경로를 제공하는 웹 서비스가 있다고 하자.
이 서비스를 이용하는 사용자는 출발역과 도착역을 설정하고 최단 경로를 찾는 버튼을 누른다.
이 때 최단 거리 경로를 구하는 서비스를 이용하기 위한 요청이 향하는 URI가, 엔드포인트이다.
이 웹 서비스는 유효한 형태로 엔드포인트에 요청이 전달되었을 경우 사용자가 알 필요 없는 서비스 내부 로직을 실행하고 응답을 반환한다.

#### API vs Endpoint?

결국 API가 두 시스템(어플리케이션)이 상호작용(소통) 할 수 있게 하는 프로토콜의 총 집합이라면, ENDPOINT는 API가 서버에서 리소스에 접근할 수 있도록 가능하게 하는 URL이라 할 수 있겠다.
<img src="https://postfiles.pstatic.net/MjAyMTA2MTdfMjAy/MDAxNjIzODk4ODYyNTg3.XOuG3T6VKIDbgmnvcdHhArnhPLprsWFKn-KwxGi0AvUg.8qSDRytl2qg-YnYmBCGiPtXFi7Y2myY7A4bP2YCILbgg.PNG.ghdalswl77/image.png?type=w773">

[출처: API 와 Endpoint ?](https://blog.naver.com/PostView.naver?blogId=ghdalswl77&logNo=222401162545&parentCategoryNo=&categoryNo=90&viewDate=&isShowPopularPosts=true&from=search)
