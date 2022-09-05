<목차>

- [React의 장점](#javascript의-프레임워크로-react의-장점-사용하는-이유)
- [React의 특징](#react의-특징은)
- [SPA란?](#spa란-무엇인가요-react의-작동방법은)
- [클래스 컴포넌트 vs 함수형 컴포넌트](#클래스-컴포넌트와-함수형-컴포넌트의-차이는-무엇인가)
- [key는 어떻게 사용되는지?](#key는-어떻게-사용되는지)
- [state와 props의 차이](#state와-props의-차이)
- [props drilling에 대해서](#prop-drilling은-무엇이고-어떻게-피할-수-있나요)
- [제어 컴포넌트 vs 비제어 컴포넌트](#제어-컴포넌트와-비제어-컴포넌트의-차이는-무엇인가요)
- [서버사이드렌더링 이란?](#서버-사이드-렌더링이란--spa와-서버-사이드-렌더링의-차이는)
- [SSR과 SSG의 차이?](#ssr과-ssg의-차이는)

# javascript의 프레임워크로 React의 장점? (사용하는 이유)

1. javascript의 프레임 워크 중 전세계 사용자가 가장 많은건 64%로 (2020년 조사결과) 가장 많다. 커뮤니티가 크다.
2. 코드의 재사용성과 유지보수성이 높은 UI를 만드는데 용이하다.
3. 규모가 크고 빠른 웹 애플리케이션을 만들 수 있다.

# React의 특징은?

- 단방향 데이터의 흐름
- virtual DOM을 사용
- UI component를 기반

# SPA란 무엇인가요? React의 작동방법은?

## SPA란?

어떤 웹 사이트의 전체 페이지를 하나의 페이지에 담아 동적으로 화면을 바꿔가며 표현하는 것이 SPA이다.

## Virtual Dom이란?

React는 Virtual DOM을 활용해 실제 DOM에 접근하여 조작하는 대신, 이를 추상화한 자바스크립트 객체를 구성하여 사용한다. 즉 동적으로 데이터가 변화했을 때 직접적으로 DOM을 조작하는 것이 아니라 DOM의 사본이라고 할 수 있는 새로운 Virtual DOM을 생성한다. 그리고 새로 생성된 Virtual DOM과 이전에 저장된 Virtual DOM을 비교해 변경된 부분의 DOM 만을 변경한다. 이 과정을 조화 과정(reconciliation)이라고 한다.
= React의 특징을 살펴보면 SPA(Single Page Application) 으로 매번 처음부터 새로운 html로 화면을 받아오는 방식을 취하는게 아니고, 가상의 DOM을 만들어서 업데이트되는 내용만 다시 그려서 UI를 보여주게 되는 특징이있다.

생성(mounting) -> 업데이트(updating) -> 제거(unmounting)의 생명주기를 가지고, 생명주기의 때에 따라 어떤 작업을 처리해야 하는지 지정해줘야 불필요한 업데이트를 방지할 수 있다.

## React가 렌더링을 실행하는 과정?

1. props가 변경되었을 때
2. state가 변경되었을 때
3. `forceUpdate()` 를 실행했을 때
4. 부모 컴포넌트가 렌더링 되었을 때

# 클래스 컴포넌트와 함수형 컴포넌트의 차이는 무엇인가?

<b>클래스 컴포넌트</b>
React 16.8(hooks 도입) 이전에는 내부 state를 유지하는 데 필요한 컴포넌트를 생성하거나 생명주기 메소드(lifecycle methods)(즉, componentDidMount 및 shouldComponentUpdate)를 활용하기 위해 클래스 기반 컴포넌트를 사용했습니다. 클래스 기반 컴포넌트는 리액트의 Component 클래스를 확장하는 ES6 클래스입니다. 또한 최소한 render() 메서드를 포함해야 합니다.

<b>함수 컴포넌트</b>
(hooks 도입 이전의) 함수형 컴포넌트는 state를 갖지 않으며 렌더링할 출력 결과를 리턴(반환)합니다. 함수형 컴포넌트는 클래스 기반 컴포넌트보다 심플하기 때문에 props에만 의존하는 UI을 렌더링하는데 선호됩니다.

# key는 어떻게 사용되는지?

리액트에서 collection을 렌더링할 때 엘리먼트와 데이터 사이의 관계를 추적하기 쉽도록 반복되는 각 엘리먼트에 key를 추가하는 것이 중요합니다. 키는 고유한 ID(이상적으로는 UUID 또는 기타 고유 문자열)를 사용해야 한다. key를 사용하지 않으면 collection에 item을 추가하거나 제거할 때 예상치 못한 동작 결과가 발생할 수 있습니다.

# state와 props의 차이?

props는 부모 컴포넌트에서 자식 컴포넌트로 전달되는 데이터입니다. props는 수정될 수 없으며 표시되거나 다른 값을 계산하는데만 사용됩니다. state는 컴포넌트의 생명 주기 동안 수정될 수 있는 내부 데이터로, 다시 렌더링해도 유지됩니다.

# prop drilling은 무엇이고 어떻게 피할 수 있나요?

prop drilling은 부모 컴포넌트에서 하위 컴포넌트(자식 컴포넌트의 자식 컴포넌트 등으)로 데이터를 전달할 때 발생하는 것으로, props를 전달하는 것 외에는 props를 필요로 하지 않는 다른 컴포넌트를 통해 “drilling”(내리꽂기) 됩니다.

# 제어 컴포넌트와 비제어 컴포넌트의 차이는 무엇인가요?

대부분 경우에 폼을 구현하는데 제어 컴포넌트를 사용하는 것이 좋습니다. 제어 컴포넌트에서 폼 데이터는 React 컴포넌트에서 다루어집니다. 대안인 비제어 컴포넌트는 DOM 자체에서 폼 데이터가 다루어집니다.

모든 state 업데이트에 대한 이벤트 핸들러를 작성하는 대신 비제어 컴포넌트를 만들려면 ref를 사용하여 DOM에서 폼 값을 가져올 수 있습니다.

비제어 컴포넌트는 DOM에 신뢰 가능한 출처를 유지하므로 비제어 컴포넌트를 사용할 때 React와 non-React 코드를 통합하는 것이 쉬울 수 있습니다. 빠르고 간편하게 적은 코드를 작성할 수 있지만, 그 외에는 일반적으로 제어된 컴포넌트를 사용해야 합니다.

ex)

```jsx
export default function App() {
  const inputRef = useRef(); // ref 사용
  const onClick = () => {
    console.log(inputRef.current.value);
  };

  return (
    <div className="App">
      <input ref={inputRef} />
      <button type="submit" onClick={onClick}>
        전송
      </button>
    </div>
  );
}
```

비제어 컴포넌트는 값이 실시간으로 동기화 되지 않는다. 만약 a와 b라는 컴포넌트가 있을 때, a에 대한 변활르 즉각적으로 b가 영향을 받아야 할때 비제어 컴포넌트는 이런 방식에 대응할 수 없다.<br>
제어 컴포넌트의 경우 사용자가 입력을 하는 액션을 취할때마다 리렌더링을 발생시키는 반면, 비제어 컴포넌트는 사용자가 직접 트리거 하기 전까지는 리렌더링을 발생시키지 않고 값을 동기화 시키지도 않는다.

- useRef와 리렌더링

1. useRef() 는 heap영역에 저장되는 일반적인 자바스크립트 객체이다.
2. 매번 렌더링할 때 동일한 객체를 제공한다. heap에 저장되어 있기 때문에 어플리케이션이 종료되거나 가비지 컬렉팅될 때 까지, 참조할때마다 같은 메모리 값을 가진다고 할 수 있다.
3. 값이 변경되어도 리렌더링이 되지 않는다. 같은 메모리 주소를 갖고있기 때문에 자바스크립트의 === 연산이 항상 true 를 반환한다. 즉 변경사항을 감지할 수 없어서 리렌더링을 하지 않는다는 뜻이다.

<b>제어 컴포넌트</b><br>
제어 컴포넌트의 값은 항상 최신값을 유지한다. 새로운 입력 값이 생길때 마다 상태를 새롭게 갱신한다. 이는 데이터와 UI에서 입력한 값이 항상 동기화됨을 알 수 있다.

<b>비제어 컴포넌트</b><br>
필드에서 값을 트리거 해야 값을 얻을 수 있다. 예를 들면, 버튼을 클릭하면 값이 갱신된다. 버튼을 클릭해 트리거 하기 전까지의 값은 변경되지 않는다.

# 서버 사이드 렌더링이란? (+ SPA와 서버 사이드 렌더링의 차이는?)

## SSR은?

-> 서버로부터 완전하게 만들어진 html파일을 받아와 페이지 전체를 렌더링 하는 방식

- 서버로부터 화면을 렌더링 하기 위한 필수적인 요소를 먼저 가져오기 때문에 이후에 설명할 클라이언트 사이드 렌더링 보다 초기로 로딩 속도가 빠르다.
- 서버측 부하가 증가한다.
- 사용자 경험이 떨어질 수 있다.

## CSR은?

-> 클라이언트 사이드 렌더링이란 사용자의 요청에 따라 필요한 부분만 응답 받아 렌더링 하는 방식이다.

- 초기 로딩시간이 더 오래 걸린다.
- 빠른 속도와 서버 부하 감소
- 사용자 친화적

## SSR과 SSG의 차이는?

## Next.js

= Next js는 간단하게 SPA에 SSR을 사용할 수 있도록 하는 프레임워크다.

NEXT는 브라우저에 렌더링 할 때 기본적으로 pre-redering(사전 렌더링)을 한다고 소개한다(이는 NEXT의 default로 설정되어 있다). pre-rendering이란 각 페이지들을 사전에 미리 HTML 문서로 생성하여 가지고 있는 것이다. 즉 Pure React에서 CSR 방식은 번들링 된 js가 클라이언트 단에서 모든 추가 렌더링을 담당했다면 Next의 pre-rendering 시스템에서는 빌드 타임 때 해당하는 페이지 별로 각각의 HTML 문서를 미리 생성해 가지고 있다가 서버로 요청이 들어올 때 알맞은 페이지를 반환해준다.

![](https://velog.velcdn.com/images/longroadhome/post/183a4341-072f-4208-a898-20aaf7a60d6a/312312.png)
![](https://velog.velcdn.com/images/longroadhome/post/5cd7fc0d-63b3-47cc-97b8-e6c85894add4/123123.png)

Next에서 pre-rendering을 하기 위해 두 가지 형식이 있다. 두 방식은 Next에서 pre-rendering을 어떻게 그리고 언제 제공하는지에 대한 차이이다.

- Static-Generation (추천) : **HTML을 빌드 타임에 각 페이지별로 생성하고 해당 페이지로 요청이 올 경우 이미 생성된 HTML 문서를 반환**한다.
- Server-Side-Rendering : **요청이 올 때 마다 해당하는 HTML 문서를 그때 그때 생성하여 반환**한다.

Next 공식문서에서는 만약 데이터의 변동이 매우 빈번하게 일어난다면 굳이 (데이터에 대한) pre-rendering을 취하지 말고 기존 pure react에서 처럼 data-fetching을 통해 클라이언트 사이드에서 렌더링 할 것을 권고하고 있다(물론 첫 페이지 일부는 Static Generation일 것이다. 아무 설정하지 않는다면 Static Generation이 default 값 이므로). 공식문서에서는 유저 대시보드에 이러한 전략을 취할 것을 권고한다. 유저 대시보드는 일단 개인적인 영역이면서 특정 유저에게 귀속되며 외부 노출이 필요하거나 SEO를 적용해야할 필요가 거의 없다. 또한 유저의 수정을 통해 즉각적으로 출력되는 화면이 변동하기에 유저 대시보드와 같은 경우 CSR 방식으로 운용하는 것이 좋은 접근 방법이 될 수 있다. 즉 정리하자면 Next 라는 프레임워크에서는 SSR 지원 방식을 두 가지로 나누어 SSR + SSG 로 세분화 한 전략을 취하고 있다고 생각하면 좋을 것 같다.

### SSG(Static Site Generation)

![](https://velog.velcdn.com/images/longroadhome/post/2b082fb2-ca4f-487d-a3d7-d6211e2c14f3/fsfsdbsdfse.png)
Static-Generation(또는 SSG) 방식은 빌드 타임(npm run build 시) 우리가 pages 폴더에서 작성한 각 페이지들에 대한 각각의 HTML 문서를 생성해서 static 문서로 가지고 있게 된다. 이 페이지에 대한 유저들의 요청이 발생하게 되면, 요청에 따라 계속 서버에서 재생성 하는 것이 아니라 이미 생성이 완료된 페이지를 반환해주게 된다. 따라서 생성이 완료된 HTML 문서를 재활용 하기에 응답 속도가 매우 빠르다. Next에서는 다음과 같은 경우에 Static-Generation 을 사용할 것을 권고하고 있다.

퍼포먼스에 집중 (CDN을 통해 더 빠른 응답 가능)
마케팅 페이지 / 블로그 게시물 / 제품의 목록 등과 같이 정적 생성하여 각 요청에 동일한 문서를 반환할 수 있는 경우

### SSR (Server Side Rendering)

![](https://velog.velcdn.com/images/longroadhome/post/9137471c-0491-41c2-bd59-f9d1cd0a2811/adfasdf.png)
SSR 방식은 유저의 요청 때 마다 그에 상응하는 HTML 문서를 생성하여 반환하는 방식이다. 즉 이전 포스팅에서 계속 설명해오던 바로 그 방식을 말한다. SSR을 사용하는 경우는 다음과 같이 설명하고 있다.

항상 최신 상태를 유지해야 하는 경우 (요청에 따라 응답해야 할 내용이 시시각각 변함)
제품의 상세 페이지 / 분석 차트 등 요청 마다 다른 내용 또는 형식의 HTML 문서가 반환되는 경우

[출처: [FE] SSR(Server-Side-Rendering) 그리고 SSG(Static-Site-Generation) (feat. NEXT를 중심으로)](https://velog.io/@longroadhome/FE-SSRServer-Side-Rendering-%EA%B7%B8%EB%A6%AC%EA%B3%A0-SSGStatic-Site-Generation-feat.-NEXT%EB%A5%BC-%EC%A4%91%EC%8B%AC%EC%9C%BC%EB%A1%9C#1-cra)

---

[출처: React 인터뷰 대비 질문과 답변 15](https://velog.io/@dojunggeun/React-interview-questions-15)
