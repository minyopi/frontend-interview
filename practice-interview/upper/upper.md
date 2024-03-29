# 프론트엔드 면접 준비

## 면접 중요도 (상)

<목차>

- [CORS에러](#cors를-대처하는-방법과-우회하는-방법을-알려주세요)
- [인터넷 vs 웹](#인터넷-vs-웹)
- [HTTP란](#http-기초-지식)
- [REST API](#rest-api란)
- [Web socket 이란?](#웹-소켓-websocket-이란)
- [객체 지향 프로그래밍](#객체-지향-프로그래밍이란)
- [함수형 프로그래밍](#함수형-프로그래밍)
- [GET과 POST의 차이](#get과-post의-차이)

### CORS를 대처하는 방법과 우회하는 방법을 알려주세요.

#### CORS에러가 발생하는 이유?

-> SOP (Same-Origin Policy) "동일 출처 정책" 때문이다. 정책명 그대로 동일 출처의 리소스 (HTTP, IMG, CSS... 등)만을 요청할 수 있습니다. 그렇기 때문에 다른 출처의 데이터를 요청을 한다는 것은 정책에 위배되는 행위라고 볼 수 있습니다. 보안을 위한 장치.
SOP의 출처는 "출처 결정 규칙"에 의해서 동일 출처인지 판단할 수 있습니다. 동일한 출처는 프로토콜, 호스트, 포트가 동일할 경우에 대해서 같은 출처로 브라우저는 인식하게 됩니다.

#### CORS (Cross-Origin Resouce Sharing)

-> CORS는 동일한 도메인이 아닌 다른 도메인에 리소스를 요청할 시에 서로 다른 origin에 대하여 HTTP 요청이 가능하게 해주는 표준입니다.
브라우저에서는 보안상의 이유로 다른 도메인에서 허용하지 않은 요청에 대하여 제한하고 있습니다. 일반적으로 다른 도메인 상에 대한 데이터를 요청을 하게 될 경우 SOP에 의하여 제한 되게 됩니다. 서버 측에서 외부 요청에 대하여 완화적인 조치를 취하게 될 경우 다른 도메인에 대한 접근할 수 있게 됩니다.

#### CORS에러 대응 방법

1. <b>Access-Control-Allow-Origin 설정</b>
   보통 CORS 이슈가 발생한다면 서버 측에서 Access-Control-Allow-Origin 헤더에 접근권한을 설정할 수 있습니다.
   `*`를 설정하게 된다면 모든 외부 출처에서 접속을 할 수 있게 됩니다. 이 방법은 당장은 편리하여 좋아보이지만 보안적인 이슈에 직면할 수 있기 때문에 이러한 방법은 지양해야겠습니다.
   그렇기에 외부에서 사용한다는 요청에 대한 심사를 거친 후 Access-Control-Allow-Origin에 외부 출처를 일일이 적용하는것이 좋습니다.
2. <b>JSONP 설정</b>
   다른 도메인에 접근할 수 있는 우회적인 기법 중에 JSONP(JSON with Padding) 방법이 있습니다. 웹 브라우저에서 실행되는 Javascript는 통신을 이용해 외부 출처에서 데이터를 받아오는 것이 불가능하지만, HTML `<script>` 요소는 외부 출처로 부터 조회된 내용을 실행하는 것이 허용되고 있습니다. 다만 Javascript 문법 오류가 발생하게 됩니다.

   문법 오류가 발생하는 이유는 Javascript에서 변수, 상수로 정의 되지 않고 json형식이 입력되면서 발생하게 됩니다.

   JSONP는 이러한 웹브라우저 특성을 이용하여 json 데이터를 서버가 콜백함수로 감싸 javascript 문법을 유효하게 만들어 전달하여 클라이언트에서 응답을 받을 수 있게 됩니다.

3. <b>Proxy 설정</b>
   외부 도메인서버에 접근하고자할 때 바로 외부 도메인 서버를 통하는 것이 아닌 자신의 서버를 매개로 하여 외부서버에 요청하는 방식입니다.

   서버에서 요청을 하게될 때에는 브라우저의 규약인 CORS 정책에 영향을 받지 않습니다. 그러한 이점을 이용하여 Proxy Server라는 출처를 통하기 때문에 CORS 정책을 위반하지 않게되어 우회 할 수 있게됩니다.

[출처: Frontend에서 Cors 해결방법](https://devport.tistory.com/13)

---

### 인터넷 vs 웹?

<b>인터넷은 컴퓨터가 서로 연결되어 통신을 주고받는 컴퓨터끼리의 네트워크를 일컫는 말</b>이고, <b>웹은 그 인터넷상에 정보가 얽혀있는 무형의 정보 네트워크를 말한다.</b>
웹은 인터넷상에서 존재하는 하나의 서비스이다. 웹은 인터넷의 일부라고 볼 수 있다.

---

### HTTP 기초 지식

#### HTTP (HyperText Transfer Protocol)란?

인터넷에서 데이터를 주고받을 수 있는 프로토콜(규칙) 입니다.
이렇게 규칙을 정해두었기 때문에, 모든 프로그램이 이 규칙에 맞춰 서로 정보를 교환할 수 있게 되었습니다.

#### HTTP 요청 (request)

웹 브라우저에서 웹 페이지를 열고 폼에 내용을 입력하면 웹 서버와 웹 브라우저가 데이터를 교환합니다.

이 교환은 HTTP에 근거해 동작하게 되고 웹 브라우저는 웹 브라우저의 정보와 폼 입력 데이터 등의 데이터 헤더를 붙여 오픈할 웹페이지의 주소를 웹 서버에 요구합니다. 이게 바로 HTTP 요청(request)입니다.

#### HTTP 응답 (response)

웹 페이지의 요청을 받은 웹 서버는 서버 정보 or 처리 결과를 나타내는 오류 코드와 메시지의 헤더를 웹 페이지 콘텐츠에 붙여 응답합니다. 이것이 HTTP 응답(response)입니다.

#### HTTP의 특징

1.  <b>비연결성 ( Connectionless )</b>
    비연결성은 클라이언트와 서버가 한 번 연결을 맺은 후, 클 라이언트 요청에 대해 서버가 응답을 마치면 맺었던 연결을 끊어 버리는 성질을 말합니다.

    - <b>비연결성의 장점</b>

      HTTP는 인터넷 상에서 불특정 다수의 통신 환경을 기반으로 설계되었습니다. 만약 서버에서 다수의 클라이언트와 연결을 계속 유지해야 한다면, 이에 따른 많은 리소스가 발생하게 됩니다.
      따라서 연결을 유지하기 위한 리소스를 줄이면 더 많은 연결을 할 수 있으므로 비연결적인 특징을 갖습니다.

    - <b>비연결성의 단점</b>
      서버는 클라이언트를 기억하고 있지 않으므로 동일한 클라이언트의 모든 요청에 대해, 매번 새로운 연결을 시도/해제의 과정을 거쳐야하므로 연결/해제에 대한 오버헤드가 발생한다는 단점이 있습니다.

    - <b>KeppAlive</b>
      이에 대한 해결책으로 오버헤드를 줄이기 위해 HTTP의 KeepAlive 속성을 사용할 수 있습니다.
      KeepAlive는 지정된 시간동안 서버와 클라이언트 사이에서 패킷 교환이 없을 경우, 상대방의 안부를 묻기위해 패킷을 주기적으로 보내는것을 말합니다. 이 때 패킷에 반응이 없으면 접속을 끊게 됩니다.
      주기적으로 클라이언트의 상태를 체크한다는 것으로 미루어보아 KeepAlive 역시 완벽한 해결책은 아닙니다.KeepAlive 속성이 On 상태라해도, 서버가 바쁜 환경에서는 프로세스 수가 기하급수적으로 늘어나기 때문에 KeepAlive로 상태를 유지하기 위한 메모리를 많이 사용하게 되므로 주의해야 합니다.

2.  <b>무상태 ( Stateless )</b>
    Connectionless로 인해 서버는 클라이언트를 식별할 수가 없는데, 이를 Stateless라고 합니다.

[출처: HTTP의 기초 지식 ( 요청 & 응답 ) ](https://choseongho93.tistory.com/164?category=803676)
[출처:[HTTP] HTTP 특성(비연결성, 무상태)과 구성요소 그리고 Restful API](https://victorydntmd.tistory.com/286)
[관련 참고 레퍼런스: 프런트엔드 개발자가 알아야하는 HTTP 프로토콜 Part 1](https://joshua1988.github.io/web-development/http-part1/)

---

### REST API란?

#### REST API?

##### REST API 탄생

REST는 Representational State Transfer라는 용어의 약자이다. REST는 네트워크 아키텍처 원리의 모음이다. 여기서 '네트워크 아키텍처 원리'란 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 일컫는다.
2000년도에 로이 필딩은 HTTP의 주요 저자 중 한 사람으로 그 당시 웹(HTTP) 설계의 우수성에 비해 제대로 사용되어지지 못하는 모습에 안타까워하며 웹의 장점을 최대한 활용할 수 있는 아키텍처로써 REST를 발표했다

##### REST의 구성

- <b>자원(RESOURCE) - URI</b> = HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
- <b>행위(Verb) - HTTP METHOD</b> = HTTP Method(POST, GET, PUT, DELETE)를 통해
- <b>표현(Representations)</b> = 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.

##### REST 의 특징

1. <b>Uniform (유니폼 인터페이스)</b>
   Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일을 말합니다.

2. <b>Stateless (무상태성)</b>
   REST는 무상태성 성격을 갖습니다. 다시 말해 작업을 위한 상태정보를 따로 저장하고 관리하지 않습니다. 세션 정보나 쿠키정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 들어오는 요청만을 단순히 처리하면 됩니다. 때문에 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 구현이 단순해집니다.

3. <b>Cacheable (캐시 가능)</b>
   REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능합니다. 따라서 HTTP가 가진 캐싱 기능이 적용 가능합니다. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능합니다.

4. <b>Self-descriptiveness (자체 표현 구조)</b>
   REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것입니다.

5. <b>Client - Server 구조</b>
   REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 됩니다.

6. <b>계층형 구조</b>
   REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 합니다.

##### REST API 디자인 가이드

REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있습니다.

첫 번째, <b>URI는 정보의 자원을 표현</b>해야 한다.
두 번째, <b>자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현</b>한다.

##### REST의 장단점

##### 장점

- HTTP 프로토콜의 인프라를 그대로 사용하므로 REST API 사용을 위한 별도의 인프라를 구출할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해 준다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 명확하게 나타내므로 의도하는 바를 쉽게 파악할 수 있다.
- 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화한다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

##### 단점

- 표준이 자체가 존재하지 않아 정의가 필요하다.
- 사용할 수 있는 메소드가 4가지밖에 없다.
- HTTP Method 형태가 제한적이다.
- 브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 정보의 값을 처리해야 하므로 전문성이 요구된다.
- 구형 브라우저에서 호환이 되지 않아 지원해주지 못하는 동작이 많다.(익스폴로어)

#### RESTful API?

<b>RESTFUL이란 REST의 원리를 따르는 시스템을 의미</b>합니다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아닙니다. REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며 모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있습니다.

[출처: REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
[[네트워크] REST API란? REST, RESTful이란?
](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)

---

### 웹 소켓 (WebSocket) 이란?

#### 웹소켓(WebSocket)의 배경

인터넷이 나오고 HTTP를 통해서 서버로부터 데이터를 가져오기 위해서는 오로지 URL을 통한 요청이 유일한 방법이었습니다. 때문에 아이디 중복 확인과 같은 유효성 검사는 서버로 데이터를 보내는 중간과정에서 새로운 페이지 요청을 하게 되었습니다.

여기서 발전된 방식이 Ajax통신으로 클라이언트에서 XMLHttpRequest 객체를 이용하여 서버에 요청을 보내면 서버가 응답을 하는 방식입니다.페이지 요청이 아닌 데이터 요청이라 부분적으로 정보를 갱신할 수 있게 됩니다.

즉, 사용자의 이벤트로부터 Javascript는 사용자가 작성한 값이 쓰여진 DOM을 읽습니다.

그리고 XMLHttpRequest 객체를 통해 웹서버에 해당 값을 전송하고 웹서버는 요청을 처리하고 XML, Text, JSON 등을 이용하여 XMLHttpRequest 객체에 전송합니다. 그런다음 JavaScript가 해당 응답정보를 DOM에 쓰여집니다.

Ajax를 사용하면 새로운 HTML을 서버로부터 받아야하는 것이 아닌 동일한 페이지의 일부를 수정할 수 있는 가능성이 생기고, 사용자 입장에서는 페이지 이동이 발생되지 않고 페이지 내부 변화만 일어나게 해주므로 그만큼의 자원과 시간을 아낄수 있습니다.

하지만, Ajax도 결국 HTTP를 이용하기 때문에 요청을 보내야 응답이 옵니다. 변경된 데이터를 가져오기 위해서 버튼을 누른다거나 일정 시간 주기로 요청을 보낸다면 번거로울 뿐더러 자원 낭비입니다.
예를 들어 주식에서 기업의 주가를 보려면 매번 버튼을 갱신해서 요청을 하고 서버는 이에 응답을 해주는 것 입니다.

이러한 문제들을 해결하기 위해 웹소켓이 탄생합니다.

#### 웹소켓(WebSocket)의 개념

<b>Transport protocol의 일종으로 서버와 클라이언트 간의 효율적인 양방향 통신을 실현하기 위한 구조</b>입니다.

웹소켓은 단순한 API로 구성되어있으며, 웹소켓을 이용하면 하나의 HTTP 접속으로 양방향 메시지를 자유롭게 주고받을 수 있습니다.

위 배경에서 웹소켓이 나오기 이전에는 모두 클라이언트의 요청이 없다면, 서버로부터 응답을 받을 수 없는 구조였습니다.

웹소켓은 이러한 문제를 해결하는 새로운 약속이었습니다.

웹소켓에서는 서버와 브라우저 사이에 양방향 소통이 가능합니다. 브라우저는 서버가 직접 보내는 데이터를 받아들일 수 있고, 사용자가 다른 웹사이트로 이동하지 않아도 최신 데이터가 적용된 웹을 볼 수 있게 해줍니다. 웹페이지를 ‘새로고침’하거나 다른 주소로 이동할 때 덧붙인 부가 정보를 통해서만 새로운 데이터를 제공하는 웹서비스 환경의 빗장을 본질적으로 풀어준 셈입니다.

웹에서도 채팅이나 게임, 실시간 주식차트와 같은 실시간이 요구되는 응용프로그램의 개발을 한층 효과적으로 구현할 수 있게 됩니다.

가상화폐의 분산화 기술의 핵심도 WebSocket으로 구현할 수 있습니다.

#### 작동원리

서버와 클라이언트간의 웹소켓 연결을 HTTP프로토콜을 통해 이루어집니다.

연결이 정상적으로 이루어진다면 서버와 클라이언트 간에 웹소켓 연결(TCP/IP기반)이 이루어지고 일정 시간이 지나면 HTTP연결은 자동으로 끊어집니다.

기본적으로 웹소켓 API는 아주 간단한 기능들만을 제공하기 때문에 대부분의 경우 SockJS나 Socket.IO같은 오픈 소스 라이브러리를 많이 사용하고 있으며 메시지 포맷 또한 STOMP같은 프로토콜을 같이 이용합니다.

#### 문제점

1. 프로그램 구현에 보다 많은 복잡성을 초래합니다.
   -> 웹 소켓은 HTTP와 달리 Stateful protocol이기 때문에 서버와 클라이언트 간의 연결을 항상 유지해야 하며 만약 비정상적으로 연결이 끊어졌을때 적절하게 대응해야 한다. 이는 기존의 HTTP 사용시와 비교했을때 코딩의 복잡성을 가중시키는 요인이 될 수 있습니다.

2. 서버와 클라이언트 간의 Socket 연결을 유지하는 것 자체가 비용이 듭니다.
   -> 특히나 트래픽 양이 많은 서버같은 경우에는 CPU에 큰 부담이 될 수 있습니다.

3. 오래된 버전의 웹 브라우저에서는 지원하지 않습니다. (물론 SockJS 라이브러리 같은 경우에는 Fallback option을 제공하고 있습니다.)

[출처: [웹소켓] WebSocket의 개념 및 사용이유, 작동원리, 문제점](https://choseongho93.tistory.com/266)

---

## 객체 지향 프로그래밍이란?

<b>객체 지향 프로그래밍</b>은 <b>컴퓨터 프로그래밍 패러다임중 하나로, 프로그래밍에서 필요한 데이터를 추상화시켜 상태와 행위를 가진 객체를 만들고 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법</b>이다.

그 단어를 사물(Object)이라는 단어로 바꾸면 조금 쉬워진다.

<b>객체지향 프로그래밍은 쉽게 말하면 실제로 우리가 사물을 바라보는 관점, 그리고 그 사물들의 연계성을 생각하는 관점을 프로그래밍에 적용하여 모델링하는 패러다임</b>을 말한다고 생각한다.

이러한 관점을 프로그래밍에 도입하면,
함수들의 집합 혹은 변수들의 목록을 관계성있는 객체들의 집합으로 분류(Classification)하고, 각 분류는 메시지를 받을 수도 있고, 데이터를 처리할 수도 있으며, 또 다른 분류에게 메시지를 전달할 수도 있게 만들 수 있는 것이다. 그리고 이것 하나하나를 객체라고 하는 것이다.

객체지향 프로그래밍은 <b>보다 유연하고 유지보수하기 쉬우며 확장성 측면에서서도 유리한 프로그래밍을 하도록 의도</b>되었다고 볼 수 있다.

이를 위해 <b>캡슐화(Encapsulation), 정보은닉(Information Hiding), 추상화(Abstraction), 상속성(Inheritance)</b> 등의 특징들을 가지고 있다.

일반적으로 JavaScript에서 객체지향 프로그래밍을 말한다면 Prototype을 통해 객체를 다루는 것을 말한다.

## 함수형 프로그래밍?

<b>함수형 프로그래밍</b>은 <b>순수 함수(pure function)를 조합하고 공유 상태(shared state), 변경 가능한 데이터(mutable data) 및 부작용(side-effects)을 피하여 프로그래밍하는 패러다임</b>이다.</br>
= 함수형 프로그래밍은 **순수 함수**와 **보조 함수**의 조합을 통해 외부 상태를 변경하는 부수효과를 최소화해서 불변성을 지향하는 프로그래밍 패러다임이다. 로직 내에 존재하는 **조건문과 반복문을 제거**해서 복잡성을 해결하며, **변수 사용을 억제**하거나 **생명주기를 최소화**해서 상태 변경을 피해 오류를 최소화하는 것을 목표로 한다. 조건문이나 반복문은 로직의 흐름을 이해하기 어렵게 해서 가독성을 해치고, 변수의 값은 누군가에 의해 언제든지 변경될 수 있어 오류 발생의 근본적인 원인이 될 수 있기 때문이다.
함수 프로그래밍은 결국 순수 함수를 통해 부수 효과를 최대한 억제해 오류를 피하고 프로그램의 안정성을 높이려는 노력의 일환이라 할 수 있다. 자바스크립트는 멀티 패러다임 언어이므로 객체지향 프로그래밍뿐만 아니라 함수형 프로그래밍을 적극적으로 활용하고 있다.

연계성을 생각하기보다는 함수를 이용해서 사이드 이펙트 없도록 선언형 프로그래밍을 하는 것이 함수형 프로그래밍인 것이다.

함수형 프로그래밍 역시 <b>순수 함수(Pure Function), 불변성(Immutable), 참조 투명성(Referential Transparency), 게으른 평가(Lazy Evaluation)등의 특징</b>이 있다.

### 예시 코드

#### 순수 함수

```js
var count = 0;

// 순수 함수 동일한 인수가 전달되면 언제나 동일한 값을 반환한다.
function increase(n) {
  return ++n;
}

// 순수 함수가 반환한 결과값을 변수에 재할당해서 상태를 변경
count = increase(count);
console.log(count); // 1

count = increase(count);
console.log(count); // 2
```

#### 비순수 함수

```js
var count = 0;

// 비순수 함수
function increase() {
  return ++count; // 외부 상태에 의존하며 외부 상태를 변경한다.
}

// 비순수 함수는 외부 상태 count를 변경하므로 상태 변화를 추적하기 어려워진다.
increase();
console.log(count);

increase();
console.log(count);
```

[출처: 객체지향 프로그래밍과 함수형 프로그래밍](https://velog.io/@huurray/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EA%B3%BC-%ED%95%A8%EC%88%98%ED%98%95-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

---

# GET과 POST의 차이?

## GET이란?

- GET 은 클라이언트에서 서버로 어떠한 리소스로 부터 정보를 요청하기 위해 사용되는 메서드이다. GET을 통한 요청은 URL 주소 끝에 파라미터로 포함되어 전송되며, 이 부분을 쿼리 스트링 (query string) 이라고 부른다.

### 특징

- GET 요청은 캐시가 가능하다.
  -> GET을 통해 서버에 리소스를 요청할 때 웹 캐시가 요청을 가로채 서버로부터 리소스를 다시 다운로드하는 대신 리소스의 복사본을 반환한다. HTTP 헤더에서 cache-control 헤더를 통해 캐시 옵션을 지정할 수 있다.
- GET 요청은 브라우저 히스토리에 남는다.
- GET 요청은 북마크 될 수 있다.
- GET 요청은 길이 제한이 있다.
  -> GET 요청의 길이 제한은 표준이 따로 있는건 아니고 브라우저마다 제한이 다르다고 한다.
- GET 요청은 중요한 정보를 다루면 안된다. ( 보안 )
  -> GET 요청은 파라미터에 다 노출되어 버리기 때문에 최소한의 보안 의식이라 생각하자.
- GET은 데이터를 요청할때만 사용 된다.

## POST란?

- POST는 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 데이터를 보낼 때 사용 되는 메서드다. POST는 전송할 데이터를 HTTP 메시지 body 부분에 담아서 서버로 보낸다. POST 로 데이터를 전송할 때 길이 제한이 따로 없어 용량이 큰 데이터를 보낼 때 사용하거나 GET처럼 데이터가 외부적으로 드러나는건 아니라서 보안이 필요한 부분에 많이 사용된다. ( 하지만 데이터를 암호화하지 않으면 body의 데이터도 결국 볼 수 있는건 똑같다. )POST를 통한 데이터 전송은 보통 HTML form 을 통해 서버로 전송된다.

### 특징

- POST 요청은 캐시되지 않는다.
- POST 요청은 브라우저 히스토리에 남지 않는다.
- POST 요청은 북마크 되지 않는다.
- POST 요청은 데이터 길이에 제한이 없다.

## 차이점

- <b>사용목적</b> : GET은 서버의 리소스에서 데이터를 요청할 때, POST는 서버의 리소스를 새로 생성하거나 업데이트할 때 사용한다. DB로 따지면 GET은 SELECT 에 가깝고, POST는 Create 에 가깝다고 보면 된다.
- <b>요청에 body 유무</b> : GET 은 URL 파라미터에 요청하는 데이터를 담아 보내기 때문에 HTTP 메시지에 body가 없다. POST 는 body 에 데이터를 담아 보내기 때문에 당연히 HTTP 메시지에 body가 존재한다.
- <b>멱등성 (idempotent)</b> : GET 요청은 멱등이며, POST는 멱등이 아니다.

#### 멱등성?

멱등의 사전적 정의는 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질을 의미한다.

GET은 리소스를 조회한다는 점에서 여러 번 요청하더라도 응답이 똑같을 것 이다. 반대로 POST는 리소스를 새로 생성하거나 업데이트할 때 사용되기 때문에 멱등이 아니라고 볼 수 있다. (POST 요청이 발생하면 서버가 변경될 수 있다.)

[출처: [네트워크] get 과 post 의 차이 ](https://noahlogs.tistory.com/35)
