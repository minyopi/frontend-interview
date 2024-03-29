<목차>

- [자바스크립트는 어떤 언어인지?](#자바스크립트는-어떤-언어인지)
- [비동기 처리란?](#비동기-처리란)
- [콜백 지옥](#콜백-지옥)
- [Promise란?](#promise-란)
- [async & await](#async--await란)
- [호이스팅](#호이스팅-이란)
- [Set과 Map의 차이](#set-과-map의-차이점은)
- [this의 용법](#this-용법에-대해서-아는대로-설명해주세요)
- [event roop란](#event-loop가-무엇이지)
- [이벤트 버블링](#이벤트-버블링에-대해서-말씀해-주세요)
- [얕은 복사와 깊은 복사](#얕은-복사shallow-copy와-깊은-복사deep-copy)

# 자바스크립트는 어떤 언어인지?

## 실제 사용시에는 멀티 스레드처럼 사용하는데 어떻게 사용하는지? 비동기적으로 실행이 되는것을 동기적으로 코딩하는 방법이 있는지?

-> 자바스크립트는 <b>싱글스레드 언어</b>이다.
멀티 스레드 처럼 사용하기 위해서는 `Web Worker`를 사용하는 방법이 있다.

# 비동기 처리란?

-> 자바스크립트의 비동기 처리란 특정 코드의 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성을 의미합니다.
이렇게 특정 로직의 실행이 끝날 때까지 기다려주지 않고 나머지 코드를 먼저 실행하는 것이 비동기 처리입니다. 자바스크립트에서 비동기 처리가 필요한 이유를 생각해보면, 화면에서 서버로 데이터를 요청했을 때 서버가 언제 그 요청에 대한 응답을 줄지도 모르는데 마냥 다른 코드를 실행 안 하고 기다릴 순 없기 때문입니다.

##비동기 처리 방식의 문제점 해결하기
-> 콜백(callback) 함수를 이용하는 것. 특정 로직이 끝났을 때 원하는 동작을 실행시킬 수 있도록 할 수 있다.

# 콜백 지옥

-> 콜백 지옥은 비동기 처리 로직을 위해 콜백 함수를 연속해서 사용할 때 발생하는 문제입니다. 웹 서비스를 개발하다 보면 서버에서 데이터를 받아와 화면에 표시하기까지 인코딩, 사용자 인증 등을 처리해야 하는 경우가 있습니다. 만약 이 모든 과정을 비동기로 처리해야 한다고 하면 위와 같이 콜백 안에 콜백을 계속 무는 형식으로 코딩을 하게 됩니다. 이러한 코드 구조는 가독성도 떨어지고 로직을 변경하기도 어렵습니다. 이와 같은 코드 구조를 콜백 지옥이라고 합니다.

# 콜백 지옥을 해결하는 방법

-> 일반적으로 콜백 지옥을 해결하는 방법에는 Promise나 Async를 사용하는 방법이 있습니다. 만약 코딩 패턴으로만 콜백 지옥을 해결하려면 각 콜백 함수를 분리해주면 됩니다.

[출처: 자바스크립트 비동기 처리와 콜백 함수](https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/)

# Promise 란?

-> 프로미스는 자바스크립트 비동기 처리에 사용되는 객체입니다.

### 예시로 알아보기

```js
function getData(callbackFunc) {
  $.get("url 주소/products/1", function (response) {
    callbackFunc(response); // 서버에서 받은 데이터 response를 callbackFunc() 함수에 넘겨줌
  });
}

getData(function (tableData) {
  console.log(tableData); // $.get()의 response 값이 tableData에 전달됨
});
```

위에 코드는 콜백 함수를 활용한 것
아래에 코드는 Promise를 적용한 것

```js
function getData(callback) {
  // new Promise() 추가
  return new Promise(function (resolve, reject) {
    $.get("url 주소/products/1", function (response) {
      // 데이터를 받으면 resolve() 호출
      resolve(response);
    });
  });
}

// getData()의 실행이 끝나면 호출되는 then()
getData().then(function (tableData) {
  // resolve()의 결과 값이 여기로 전달됨
  console.log(tableData); // $.get()의 reponse 값이 tableData에 전달됨
});
```

## 프로미스의 3가지 상태

프로미스를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 프로미스의 상태(states)입니다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미합니다. new Promise()로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖습니다.

<b>Pending(대기)</b> : 비동기 처리 로직이 아직 완료되지 않은 상태
<b>Fulfilled(이행)</b> : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
<b>Rejected(실패)</b> : 비동기 처리가 실패하거나 오류가 발생한 상태

### 프로미스 코드 예제

```js
function getData() {
  return new Promise(function (resolve, reject) {
    $.get("url 주소/products/1", function (response) {
      if (response) {
        resolve(response);
      }
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData()
  .then(function (data) {
    console.log(data); // response 값 출력
  })
  .catch(function (err) {
    console.error(err); // Error 출력
  });
```

[출처: 자바스크립트 Promise 쉽게 이해하기](https://joshua1988.github.io/web-development/javascript/promise-for-beginners/)

# async & await란?

async와 await는 자바스크립트의 비동기 처리 패턴 중 가장 최근에 나온 문법입니다. 기존의 비동기 처리 방식인 콜백 함수와 프로미스의 단점을 보완하고 개발자가 읽기 좋은 코드를 작성할 수 있게 도와준다.

### 기본 문법

```js
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

먼저 함수의 앞에 <b>async 라는 예약어</b>를 붙입니다. 그러고 나서 함수의 내부 로직 중 HTTP 통신을 하는 <b>비동기 처리 코드 앞에 await를 붙입니다.</b> 여기서 주의하셔야 할 점은 <b>비동기 처리 메서드가 꼭 프로미스 객체를 반환해야 await가 의도한 대로 동작</b>합니다.

## async & await 예외 처리

async & await에서 예외를 처리하는 방법은 바로 try catch입니다. 프로미스에서 에러 처리를 위해 .catch()를 사용했던 것처럼 async에서는 catch {} 를 사용하시면 됩니다.

[출처: 자바스크립트 async와 await](https://joshua1988.github.io/web-development/javascript/js-async-await/)

---

# `async` 와 `defer`의 차이?

- `async`는 HTML렌더링을 멈추지 않고 동시에 js파일을 다운로드 하고, <b>다운로드가 끝난 후에 자바스크립트를 실행</b>한다.
- `defer`는 HTML렌더링을 멈추지 않고 동시에 js파일을 다운로드 하고, <b>HTML렌더링이 끝난 후에 자바스크립트를 실행</b>한다.

---

# 호이스팅 이란?

-> <b>함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것</b>을 말한다.

## 호이스팅이란

- 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다.
  - 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는다.
  - 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.
  - 유효 범위: 함수 블록 `{}` 안에서 유효
- 즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
  - 실제로 코드가 끌어올려지는 건 아니며, 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이다.
    실제 메모리에서는 변화가 없다.

## 호이스팅의 대상

- <b>var 변수 선언과 함수선언문에서만 호이스팅</b>이 일어난다.
  - var 변수/함수의 <b>선언</b>만 위로 끌어 올려지며, <b>할당</b>은 끌어 올려지지 않는다.
  - let/const 변수 선언과 함수표현식에서는 ~~호이스팅이 발생하지 않는다.~~ -> 호이스팅이 발생하지 않는게 아니다.
    - `var, let, const` 모두 호이스팅이 된다.
    - 하지만, `var`는 블록 레벨 스코프를 지원하지 않고, 함수 레벨 스코프를 지원한다. (= 의도치 않게 전역 변수가 선언되어 심각한 부작용을 야기할 수 있다.)
    - `let` , `const`의 경우, 스코프에 진입할 때 변수가 만들어지고 TDZ(Temparal Dead Zone)가 생성되지만, 코드 실행이 변수가 실제 위치에 도달할 때 까지 액세스 할 수 없는것이다.
    - `let`, `const` 변수가 선언된 시점에서 제어 흐름은 TDZ를 떠난 상태가 되며, 변수를 사용할 수 있게 된다.

[참고자료: let과 const는 호이스팅 될까?](https://medium.com/korbit-engineering/let%EA%B3%BC-const%EB%8A%94-%ED%98%B8%EC%9D%B4%EC%8A%A4%ED%8C%85-%EB%90%A0%EA%B9%8C-72fcf2fac365)

#### \* TIP 호이스팅 사용 시 주의

- 코드의 가독성과 유지보수를 위해 호이스팅이 일어나지 않도록 한다.
  - 호이스팅을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅으로 인한 스코프 꼬임 현상은 방지할 수 있다.
  - let/const를 사용한다.
- var를 쓰면 혼란스럽고 쓸모없는 코드가 생길 수 있다. 그럼 왜 var와 호이스팅을 이해해야 할까?
  - ES6를 어디에서든 쓸 수 있으려면 아직 시간이 더 필요하므로 ES5로 트랜스컴파일을 해야한다.
    따라서 아직은 var가 어떻게 동작하는지 이해하고 있어야 한다.

[출처: [JavaScript] 호이스팅(Hoisting)이란](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html)

---

# Set 과 Map의 차이점은?

- 객체 – 키가 있는 컬렉션을 저장함
- 배열 – 순서가 있는 컬렉션을 저장함

## Map?

- 맵(Map)은 키가 있는 데이터를 저장한다는 점에서 객체와 유사합니다. 다만, 맵은 키에 다양한 자료형을 허용한다는 점에서 차이가 있습니다. size 프로퍼티 등의 유용한 메서드나 프로퍼티가 있습니다.

## Set?

- 셋(Set)은 중복을 허용하지 않는 값을 모아놓은 특별한 컬렉션입니다. 셋에 키가 없는 값이 저장됩니다.

[출처: 맵과 셋](https://ko.javascript.info/map-set)

---

# this 용법에 대해서 아는대로 설명해주세요.

자바스크립트의 함수는 호출될 때, 매개변수로 전달되는 인자값 이외에, arguments 객체와 this를 암묵적으로 전달 받는다.
Java에서의 this는 인스턴스 자신(self)을 가리키는 참조변수이다. this가 객체 자신에 대한 참조 값을 가지고 있다는 뜻이다. 주로 매개변수와 객체 자신이 가지고 있는 멤버변수명이 같을 경우 이를 구분하기 위해서 사용된다.

---

# 클로져는 무엇인지 설명해 보세요.

-> 클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 또는, 클로저 안에 정의된 함수는 만들어진 환경을 ‘기억한다’.

[출처: JavaScript 클로저(Closure)](https://hyunseob.github.io/2016/08/30/javascript-closure/)

---

# `Event Loop`가 무엇이지?

= 자바스크립트는 이벤트 루프를 이용해서 비동기 방식으로 동시성을 지원한다.
= **JavaScript의 런타임 모델은 코드의 실행, 이벤트의 수집과 처리, 큐에 대기 중인 하위 작업을 처리하는 이벤트 루프에 기반**하고 있으며, C 또는 Java 등 다른 언어가 가진 모델과는 상당히 다릅니다.

<시각적 표현>
![event roop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop/the_javascript_runtime_environment_example.svg)

- 스택

  - 함수 호출은 'Frame' Stack을 형성한다.

  ```js
  function foo(b) {
    let a = 10;
    return a + b + 11;
  }

  function bar(x) {
    let y = 3;
    return foo(x * y);
  }

  const baz = bar(7); // 42를 baz에 할당

  // 즉, baz에서 bar 함수 호출 스택에 들어가고,
  // bar에서 foo함수 호출 스택에 들어가고,
  // foo에서 값을 return 해서 나가고,
  // bar에서 값을 return 하고 나가고,
  // baz 의 값은 42 라는 할당을 하게 됨.
  ```

- 힙
  - 객체는 힙에 할당된다. 힙은 단순히 메모리의 큰 영역을 지칭.
- 큐
  - JavaScript 런타임은 메시지 큐, 즉 처리할 메시지의 대기열을 사용합니다. 각각의 메시지에는 메시지를 처리하기 위한 함수가 연결돼있습니다.
  - 이벤트 루프의 임의 시점에, 런타임은 대기열에서 가장 오래된 메시지부터 큐에서 꺼내 처리하기 시작합니다. 이를 위해 런타임은 꺼낸 메시지를 매개변수로, 메시지에 연결된 함수를 호출합니다.
  - 다른 함수와 마찬가지로, 호출로 인한 새로운 스택 프레임도 생성됩니다.
  - 함수 처리는 스택이 다시 텅 빌 때까지 계속됩니다. 그 후, 큐에 메시지가 남아있으면 같은 방법으로 처리를 계속 진행합니다.

## Event Roop

= 이벤트 루프는 이 기능을 구현할 때 보통 사용하는 방식에서 그 이름을 얻었으며, 대략 다음과 같은 형태입니다. `queue.waitForMessage()` 함수는 현재 처리할 수 있는 메시지가 존재하지 않으면 새로운 메시지가 도착할 때까지 동기적으로 대기합니다.

```js
while (queue.waitForMessage()) {
  // queue에서 대기중인 태스크가 있는지?
  queue.processNextMessage(); // queue에서 실행중인 태스크가 있는지?
}
```

### "Run-to-completion"

각 메시지의 처리는 다른 메시지의 처리를 시작하기 전에 완전히 끝납니다.<br>

이 특징은 프로그램의 동작을 추론할 때 유용한 특성을 제공합니다. 실행한 함수가 다른 작업에 의해 선점될 일이 없고, 다른 모든 코드의 실행보다 우선해서 값을 변경할 수 있으며, 중단되는 일 없이 완전히 끝나기 때문입니다. 반면, 예를 들어 C 언어에서는, 스레드에서 실행 중인 함수를 런타임 시스템이 임의로 멈추고 다른 스레드의 다른 코드를 먼저 실행할 수 있습니다.<br>

이 모델의 단점은, **만약 메시지를 처리할 때 너무 오래 걸리면 웹 애플리케이션이 클릭이나 스크롤과 같은 사용자 상호작용을 처리할 수 없다는 점**입니다. 브라우저는 "스크립트 응답 없음" 대화상자를 표시해서 이 문제를 완화합니다. **개발자로서 사용할 수 있는 좋은 방법으로는 메시지 처리를 가볍게 유지하고, 가능하다면 하나의 메시지를 여러 개로 나누는 것**입니다.<br>

### 메시지 추가하기

웹 브라우저에서는 수신기가 부착된 이벤트가 발생하면 새로운 메시지가 추가됩니다. 수신기가 없으면 메시지는 유실됩니다. 즉, 클릭 이벤트 처리기가 붙은 요소를 클릭하면 메시지가 새로 추가되는 식입니다. 다른 이벤트에 대해서도 마찬가지입니다.

`setTimeout` 함수는 두 개의 매개변수를 가집니다. 첫 번째는 큐에 추가할 메시지, 두 번째는 시간 값(선택 사항, 기본 값 0)입니다. 시간 값은 메시지를 큐에 추가하기까지 기다릴 (최소) 지연 시간을 나타냅니다. 큐에 다른 메시지가 없고 스택이 비어있다면 `setTimeout`의 메시지는 딜레이 직후 즉시 처리됩니다. 그러나 다른 메시지가 존재한다면 `setTimeout`은 앞선 메시지의 처리를 기다려야 합니다. 그래서 두 번째 값은 정확한 지연시간이 아닌, '최소' 지연 시간만 나타냅니다.

```js
const s = new Date().getSeconds();

setTimeout(function () {
  // "2"를 출력, 즉 500밀리초가 지난 후 즉시 실행된 것이 아니라는 것
  console.log(new Date().getSeconds() - s + "초 후 실행됨");
}, 500);

while (true) {
  if (new Date().getSeconds() - s >= 2) {
    console.log("좋아요, 2초간 반복했습니다.");
    break;
  }
}
```

### 0의 지연 시간

0의 지연 시간을 지정하는 것이 콜백을 0밀리초 후에 호출한다는 뜻은 아닙니다. `setTimeout`의 지연 시간에 0 밀리초를 지정하고 호출하더라도 콜백 함수는 즉시 실행되지 않습니다.

실제 실행 시점은 큐에서 대기 중인 작업의 수에 따라 다릅니다. 아래 예제에서는 '평범한 메시지'가 콜백의 호출보다 앞서 콘솔에 기록될 것입니다. 지연 시간은 요청을 처리하기 전에 대기할 '최소' 시간이고, 보장 시간이 아니기 때문입니다.

setTimeout에 특정 지연 시간을 지정하더라도, 큐에서 대기 중인 모든 메시지의 처리는 기다려야 합니다.

```js
(function () {
  console.log("시작");

  setTimeout(function cb() {
    console.log("콜백 1: 콜백 메시지");
  }); // has a default time value of 0

  console.log("평범한 메시지");

  setTimeout(function cb1() {
    console.log("콜백 2: 콜백 메시지");
  }, 0);

  console.log("종료");
})();

// "시작"
// "평범한 메시지"
// "종료"
// "콜백 1: 콜백 메시지"
// "콜백 2: 콜백 메시지"
```

### 논 블로킹

다른 많은 언어와 달리 **JavaScript는 절대 블로킹 연산을 하지 않습니다**. 논 블로킹은 이벤트 루프 모델의 무척 흥미로운 특징으로, 대부분의 입출력 처리가 이벤트와 콜백을 통해 수행되므로 애플리케이션이 IndexedDB 질의나 XHR 요청의 반환을 대기 중이더라도 여전히 사용자 입력 등 다른 것들을 처리할 수 있는 것입니다

[출처: MDN WEB DOCS Event Roop](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)

-> **이벤트 루프란 자바스크립트 엔진이 아닌, 구동하는 환경(브라우저, 노드)에서 가지고 있는 장치**이다. 콜 스택과 태스크 큐(= 콜백 큐)를 감시하며, 콜 스택이 비어있을 경우에 태스크 큐에서 태스크(= 콜백함수)를 가져와 콜 스택에 넣어 실행시키는 기능을 한다.
-> 자바스크립트가 '단일 스레드' 기반의 언어라는 말은 '자바스크립트 엔진이 단일 호출 스택을 사용한다'는 관점에서만 사실이다. 실제 자바스크립트가 구동되는 환경(브라우저, Node.js등)에서는 주로 여러 개의 스레드가 사용되며, <b>이러한 구동 환경이 단일 호출 스택을 사용하는 자바 스크립트 엔진과 상호 연동하기 위해 사용하는 장치가 바로 '이벤트 루프'</b>인 것이다.
-> 태스크 큐 말고도 마이크로태스크 큐 (Micro task queue)가 존재한다는 것을 알았고 이는 Promise의 동작 방식과 연관이 있다.

<b>태스크 큐 vs 마이크로태스크 큐</b>
2개의 큐 모두 콜백함수가 들어간다는 점에서 동일하지만 어떤 함수를 실행하느냐에 따라 어디로 들어가는지가 달라진다. 또한 명칭은 큐 (Queue) 이지만 실제 우리가 아는 자료구조의 큐와는 다르다. 엄밀히 말하자면 우선순위 큐 (Priority Queue) 라고 할 수 있는데, 이벤트 루프가 2개의 큐에서 태스크를 꺼내는 조건이 “제일 오래된 태스크” 이기 때문이다.

- 콜백함수를 태스크 큐에 넣는 함수들

`setTimeout, setInterval, setImmediate, requestAnimationFrame, I/O, UI 렌더링`

- 콜백함수를 마이크로태스크 큐에 넣는 함수들

`process.nextTick, Promise, Object.observe, MutationObserver`

결론부터 말하자면, <b>마이크로태스크</b>가 먼저이다.

이벤트 루프는 마이크로태스크 큐의 모든 태스크들을 처리한 다음, 태스크 큐의 태스크들을 처리한다. 따라서, Promise 의 콜백함수가 setTimeout() 의 콜백함수보다 먼저 처리된다.

[출처: 자바스크립트와 이벤트 루프](https://meetup.toast.com/posts/89)
[참고자료: [JavaScript] 런타임 작동 방식, 비동기와 이벤트 루프 ](https://hanamon.kr/javascript-%EB%9F%B0%ED%83%80%EC%9E%84-%EC%9E%91%EB%8F%99-%EB%B0%A9%EC%8B%9D-%EB%B9%84%EB%8F%99%EA%B8%B0%EC%99%80-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84/)

---

# 이벤트 버블링에 대해서 말씀해 주세요.

## 이벤트 등록

이벤트 등록이란 웹 애플리케이션에서 사용자의 입력을 받기 위해 필요한 기능

## 이벤트 버블링 - Event Bubbling

이벤트 버블링은 특정 화면 요소에서 이벤트가 발생했을 때 해당 이벤트가 더 상위의 화면 요소들로 전달되어 가는 특성을 의미합니다. 아래와 같은 그림처럼요.
<img src="https://joshua1988.github.io/images/posts/web/javascript/event/event-bubble.png">

## 이벤트 캡쳐 - Event Capture

이벤트 캡쳐는 이벤트 버블링과 반대 방향으로 진행되는 이벤트 전파 방식
<img src="https://joshua1988.github.io/images/posts/web/javascript/event/event-capture.png">

[출처: 이벤트 버블링, 이벤트 캡처 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)

---

## 얕은 복사(shallow copy)와 깊은 복사(deep copy)

객체를 프로퍼티 값으로 갖는 객체의 경우 얕은 복사는 한 단계까지만 복사하는 것을 말하고, 깊은 복사는 객체에 중첩되어 있는 객체까지 복사하는 것을 말한다.

### 참조에 의한 전달

#### 객체의 경우

```js
// 객체의 경우
var person = {
  name: "Lee",
};

// 참조 값을 복사(얕은 복사)
var copy = person;

console.log(copy === person); // true

copy.name = "Kim";
person.addres = "Seoul";

// copy와 person은 동일한 객체를 가리킨다
// 따라서 어느 한쪽에서 객체를 변경하면 서로 영향을 주고받는다.
console.log(person); // {name: 'Kim', address: 'Seoul'}
console.log(copy); // {name: 'Kim', address: 'Seoul'}

var person1 = {
  name: "Lee",
};

var person2 = {
  name: "Lee",
};

console.log(person1 === person2); // false
console.log(person1.name === person2.name); // true
```

이 경우, 객체를 가리키는 변수(원본, person)를 다른 변수(사본, copy)에 할당하면 원본의 참조 값이 복사되어 전달된다. 이를 참조에 의한 전달이라 한다.

##### 객체를 복사하는 방법

객체를 참조를 공유하지 않는 방법으로 복사하기 위해서는 `Object.assign()`과 `spread 연산자`가 있습니다.

#### 배열의 경우

```js
// 배열의 경우
const arr = ["a", "b", "c"];
const copy = arr;

arr[2] = "e";
copy[3] = "f";

console.log(arr); // ['a','b','c','e','f']
console.log(copy); // ['a','b','c','e','f']
```

##### 배열을 복사하는 방법

배열을 복사하는 방법으로는 `slice()`, `concat()`, `spread 연산자`, `Array.from()`을 사용할 수 있다.

```js
const arr1 = ["a", "b", "c"];
const arr2 = arr1.splice();

console.log(arr1 === arr2); // false

arr2[2] = "d";

console.log(arr1); // ['a','b','c']
console.log(arr2); // ['a','b','c','d']
```

출처: 모던 자바스크립트 Deep Dive
