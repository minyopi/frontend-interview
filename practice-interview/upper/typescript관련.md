<목차>

- [Typescript란?](#typescript란)
- [Typescript 공식 문서 내용](#typescript-공식-문서-내용)
  - [Union Type](#union-type)
  - [Type Aliases](#type-aliases)
  - [Interface](#interface)
  - [Type Assertions](#type-assertions)
  - [Literal Type](#literal-type)
  - [null과 undefined](#null-과-undefined)
  - [Generics](#generics)
  - [Narrowing](#narrowing)
    - [typeof type guards](#1-typeof-type-guards)
    - [truthiness narrowing](#2-truthiness-narrowing)
    - [equlity narrowing](#3-equality-narrowing)
    - [the `in` operator narrowing](#4-the-in-operator-narrowing)
    - [`instanceof` narrowing](#5-instanceof-narrowing)
    - [assignments](#6-assignments)
    - [control flow analysis](#7-control-flow-analysis)
    - [using type predicates](#8-using-type-predicates)
    - [discriminated unions](#9-discriminated-unions)
    - [the never type](#10-the-never-type)
    - [exhastiveness checking](#11-exhastiveness-checking)
- [Typescript 관련 예상 면접 질문](#typescript-관련-예상-면접-질문)
  - [alias와 interface의 차이?](#alias와-interface의-차이는)
  - [any과 unknown의 차이?](#unknown-vs-any-차이는)

## `Typescript`란?

-> 타입스크립트는 자바스크립트의 슈퍼셋인 오픈소스 프로그래밍 언어이다.

- 쉬운말로 설명을 해보자면, 타입을 명시할 필요가 없는 **동적 타입 언어**이자, **인터프리터 언어**인 비교적 유연한 자바스크립트와 달리, <b>정적 타입을 명시할 수 있다는 것이 순수한 자바스크립트와의 가장 큰 차이점</b>이다. 이로인한 장점이라 하면, 높은 개발 안정성과 편의성을 확보할 수 있다.
  그래서 대기업이나 큰 규모의 서비스를 제공하는 회사에서는 타입스크립트를 많이 사용한다. 나는 규모에 상관없이 미리 일어날 에러들에 대처 할수 있다는 것은 개발자에게도 많은 이점이 있고 생산성도 향상 될거라고 생각 되어서 관심을 가지게 되었다.
- 개발자가 의도한 변수나 함수 등의 목적을 더욱 명확하게 전달할 수 있고, 그렇게 전달된 정보를 기반으로 코드 자동 완성이나 잘못된 변수/함수 사용에 대한 에러 알림 같은 풍부한 피드백을 받을 수 있게 되므로 순수 자바스크립트에 비해 어마어마한 생산성 향상을 꾀할 수 있다. 즉, '자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것' 이 타입스크립트의 사용 목적이다.

[레퍼런스: 타입스크립트, 써야할까?](https://hyunseob.github.io/2018/08/12/do-you-need-to-use-ts/)

---

## `Typescript` 공식 문서 내용

### Union Type

= 유니언 타입은,서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로, 유니언 타입의 값은 타입 조합에 사용된 타입 중 **무엇이든 하나**를 타입으로 가질 수 있습니다. 조합에 사용된 각 타입을 유니언 타입의 **멤버**라고 부릅니다.

```ts
function checkId(id: number | string) {
  //
}
```

### Type Aliases

= 똑같은 타입을 재사용하거나 또 다른 이름으로 부르고 싶은 경우 사용한다. `type alias`를 사용하면 모든 타입에 대하여 새로운 이름을 부여할 수 있다. 단, 단지 이름에 지나지 않는다는 점에 유의해야한다.

```ts
type id = {
  x: number;
  y: number;
};
```

### Interface

= 인터페이스는 객체 타입을 만드는 또 다른 방법이다. `alias`와 마찬가지로 마치 타입이 없는 익명 객체를 사용하는 것 처럼 동작한다. Typescript는 오직 `printCoord`에 전달된 값의 **구조**에만 관심을 가진다. 즉, 예측된 프로퍼티를 가졌는지 여부만 따진다. 이처럼, 타입이 가지는 구조와 능력에만 관심을 가진다는 점은 Typescript가 **구조적** 타입 시스템이라고 불리는 이유이다.

```ts
interface Point {
  x: number;
  y: number;
}

function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}

printCoord({ x: 100, y: 100 });
```

#### `alias` vs `interface`

-> 타입 별칭과 인터페이스는 매우 유사하며, 대부분의 경우 둘 중 하나를 자유롭게 선택하여 사용할 수 있습니다. interface가 가지는 대부분의 기능은 type에서도 동일하게 사용 가능합니다. 이 둘의 가장 핵심적인 차이는, **타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다는 점**입니다. 타입은 생성된 뒤에는 달라질 수 없다.

### Type Assertions

때로는 TypeScript보다 당신이 어떤 값의 타입에 대한 정보를 더 잘 아는 경우도 존재합니다. 이런경우 `Type Assertion`(=타입 단언)을 사용해서 좀 더 구체적으로 명시할 수 있다.

```ts
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
```

이 규칙이 때로는 지나치게 보수적으로 작용하여, 복잡하기는 하지만 유효할 수 있는 강제 변환이 허용되지 않기도 합니다. 이런 경우, 두 번의 단언을 사용할 수 있습니다. any(또는 이후에 소개할 unknown)로 우선 변환한 뒤, 그다음 원하는 타입으로 변환하면 됩니다.

```ts
declare const expr: any;
type T = { a: 1; b: 2; c: 3 };
// ---중간 생략---
const a = expr as any as T;
```

### Literal Type

= string과 number와 같은 일반적인 타입 이외에도, 구체적인 문자열과 숫자 값을 타입 위치에서 지정할 수 있습니다.
= 리터럴을 유니언과 함께 사용하면, 보다 유용한 개념들을 표현할 수 있게 됩니다. 예를 들어, 특정 종류의 값들만을 인자로 받을 수 있는 함수를 정의하는 경우가 있습니다.

```ts
// ex) string ver.
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre"); // error

// ex) number ver.
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

#### Literal Inference (리터럴 추론)

객체를 사용하여 변수를 초기화하면, TypeScript는 해당 객체의 프로퍼티는 이후에 그 값이 변화할 수 있다고 가정합니다. 예를 들어, 아래와 같은 코드를 작성하는 경우를 보겠습니다.

```ts
declare const someCondition: boolean;
// ---중간 생략---
const obj = { counter: 0 };
if (someCondition) {
  obj.counter = 1;
}
```

동일한 사항이 문자열에도 적용됩니다.

```ts
const req = { url: "https://example.com", method: "GET" };
handleRequest(req.url, req.method); // Argument of type 'string' is not assignable to parameter of type '"GET" | "POST"'.
```

위 예시에서 req.method는 string으로 추론되지, "GET"으로 추론되지 않습니다. req의 생성 시점과 handleRequest의 호출 시점 사이에도 얼마든지 코드 평가가 발생할 수 있고, 이때 req.method에 "GUESS"와 같은 새로운 문자열이 대입될 수도 있으므로, TypeScript는 위 코드에 오류가 있다고 판단합니다.
해결방법은 두가지가 있다.

1. 둘 중에 한 위치에 타입 단언을 추가하여 추론 방식을 변경할 수 있습니다.

```ts
// 수정 1:
const req = { url: "https://example.com", method: "GET" as "GET" };
// 수정 2
handleRequest(req.url, req.method as "GET");
```

2. `as const`를 사용하여 객체 전체를 리터럴 타입으로 변환할 수 있습니다.

```ts
declare function handleRequest(url: string, method: "GET" | "POST"): void;
// ---중간 생략---
const req = { url: "https://example.com", method: "GET" } as const;
handleRequest(req.url, req.method);
```

`as const` 접미사는 일반적인 `const`와 유사하게 작동하는데, 해당 객체의 모든 프로퍼티에 `string` 또는 `number`와 같은 보다 일반적인 타입이 아닌 리터럴 타입의 값이 대입되도록 보장합니다.

### null 과 undefined

JavaScript에는 빈 값 또는 초기화되지 않은 값을 가리키는 두 가지 원시값이 존재합니다. 바로 `null`과 `undefined`입니다.

TypeScript에는 각 값에 대응하는 동일한 이름의 두 가지 *타입*이 존재합니다. 각 타입의 동작 방식은 `strictNullChecks` 옵션의 설정 여부에 따라 달라집니다.

#### `strictNullChecks`가 설정되지 않았을 때

`strictNullChecks`가 설정되지 않았다면, 어떤 값이 `null` 또는 `undefined`일 수 있더라도 해당 값에 평소와 같이 접근할 수 있으며, `null`과 `undefined`는 모든 타입의 변수에 대입될 수 있습니다. 이는 Null 검사를 하지 않는 언어(C#, Java 등)의 동작 방식과 유사합니다. Null 검사의 부재는 버그의 주요 원인이 되기도 합니다. 별다른 이유가 없다면, 코드 전반에 걸쳐 `strictNullChecks` 옵션을 설정하는 것을 항상 권장합니다.

#### `strictNullChecks` 설정되었을 때

`strictNullChecks`가 설정되었다면, 어떤 값이 `null` 또는 `undefined`일 때, 해당 값과 함께 메서드 또는 프로퍼티를 사용하기에 앞서 해당 값을 테스트해야 합니다. 옵셔널 프로퍼티를 사용하기에 앞서 `undefined` 여부를 검사하는 것과 마찬가지로, *좁히기*를 통하여 `null`일 수 있는 값에 대한 검사를 수행할 수 있습니다.

```ts
function doSomething(x: string | undefined) {
  if (x === undefined) {
    // 아무 것도 하지 않는다
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}
```

#### Null 아님 단언 연산자 (접미사!)

TypeScript에서는 명시적인 검사를 하지 않고도 타입에서 `null`과 `undefined`를 제거할 수 있는 특별한 구문을 제공합니다. 표현식 뒤에 !를 작성하면 해당 값이 null 또는 undefined가 아니라고 타입 단언하는 것입니다.

```ts
function liveDangerously(x?: number | undefined) {
  // 오류 없음
  console.log(x!.toFixed());
}
```

다른 타입 단언과 마찬가지로 이 구문은 코드의 런타임 동작을 변화시키지 않으므로, ! 연산자는 반드시 해당 값이 `null` 또는 `undefined`가 아닌 경우에만 사용해야 합니다.

### Generics

단일 타입이 아닌 다양한 타입에서 작동하는 컴포넌트를 작성할 수 있습니다. 사용자는 제네릭을 통해 여러 타입의 컴포넌트나 자신만의 타입을 사용할 수 있습니다.

( =>Generic은 자료형을 정하지 않고 여러 타입을 사용할 수 있게 해준다. 즉, 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 한다. 한번의 선언으로 다양한 타입에 '재사용'이 가능하다는 장점이 있다. )

제네릭을 쓰지 않을 경우, 불필요한 타입 변환을 하기 때문에 프로그램의 성능에 악영향을 미치기도 하는데, 제네릭을 사용하게되면 따로 타입 변환을 할 필요가 없어서 프로그램의 성능이 향상되는 장점이 있다.

일단 제네릭 identity 함수를 작성하고 나면, 두 가지 방법 중 하나로 호출할 수 있습니다. 첫 번째 방법은 **함수에 타입 인수를 포함한 모든 인수를 전달**하는 방법입니다.
두 번째 방법은 아마 가장 일반적인 방법입니다. 여기서는 **타입 인수 추론** 을 사용합니다 — 즉, 우리가 전달하는 인수에 따라서 컴파일러가 Type의 값을 자동으로 정하게 하는 것입니다:

```ts
function identity<Type>(arg: Type): Type {
  return arg;
}

// 1)
let output = identity<string>("myString"); // 출력 타입은 'string'입니다.

// 2)
let output = identity("myString"); // 출력 타입은 'string'입니다.
```

타입 인수를 꺾쇠괄호(<>)에 담아 명시적으로 전달해 주지 않은 것을 주목하세요; 컴파일러는 값인 "myString"를 보고 그것의 타입으로 Type를 정합니다. 인수 추론은 코드를 간결하고 가독성 있게 하는 데 있어 유용하지만 더 복잡한 예제에서 컴파일러가 타입을 유추할 수 없는 경우엔 명시적인 타입 인수 전달이 필요할 수도 있습니다.

```ts
// ex)
// number 타입의 매개변수를 return하는 함수
function NumberReturnFunc(arg: number): number {
  return arg;
}

// string 타입의 매개변수를 return하는 함수
function StringReturnFunc(arg: string): string {
  return arg;
}

// boolean 타입의 매개변수를 return하는 함수
function BooleanReturnFunc(arg: boolean): boolean {
  return arg;
}

// 이런 경우에  한개의 제네릭 타입을 사용하여 함수를 구현할 수 있다.
function GenericReturnFunc<T>(arg: T): T {
  return arg;
}

// 호출시에는 이런식으로 지정해서 사용할 수 있게 된다.
let numVar = GenericReturnFunc<number>(123);
let strVar = GenericReturnFunc<string>("ABC");

// 만약 이렇게 쓰게되면 <>를 사용하지 않고, 인수의 타입인 'string'으로 자동으로 결정
let strVar = GenericReturnFunc("ABC");
```

#### 제네릭 화살표 함수 (Generic Arrow Fuction)

```ts
// tsx 확장자 파일에서는 에러를 발생시킨다. 태그로 해석해버린다.
let GenericReturnFunc = <Type>(arg: Type): Type => {
  return arg;
};

// tsx 확장자에서 제네릭 화살표 함수를 구현해야 하는 경우
// 제네릭 매개변수에 extends를 사용하여 컴파일러에게 제네릭 화살표 함수라고 알려줘야 한다.
let GenericReturnFunc = <Type extends {}>(arg: Type): Type => {
  return arg;
};
```

[출처: 평범한 직장인의 공부 정리](https://developer-talk.tistory.com/195)

### Narrowing

= 덜 정확한 타입에서 더 정확한 타입으로 변할 수 있다. 이 과정을 **type narrowing**이라고 한다. 타입 에러를 피하기 위해 type narrowing을 사용할 수 있다.
= 컴파일과 런타임을 이해하고 안전한 앱을 만든다. type narrowing을 통해 type guard를 적극적으로 사용하면, 안전한 앱을 만들 수 있다. 타입스크립트는 컴파일 단계에서 에러를 잡는것. 런타임에는 관여하지 않는다. 런타임은 타입 가드를 통해 잡아야 한다.
= 컴파일 단계에서 에러는 `typescript`를 통해 체크하고, 런타임 단계에서는 리액트의 경우 `prop types`를 통해 체크할 수 있다. ( 과연 둘 다 사용해야 하는가에 관해서는 정답이 없다. 만일 `prop types`를 사용하지 않을때는 `typescript`의 `type guard`를 통해 런타임 에러를 적극적으로 방지 한다. )
= 왜냐하면, typescript의 **Soundness** 라는 특성 떄문이다. 타입스크립트는 런타임에 개입하지 않고 개발자에게 권한을 준다.

#### 1. `typeof` type guards

자바스크립트에서는 `typeof` operator를 지원한다. 종류는 아래와 같다.

- "string"
- "number"
- "bigint"
- "boolean"
- "symbol"
- "undefined"
- "object"
- "function"

`typeof` 연산자를 활용하여 아래와 같이 조건문으로 에러를 방지할 수 있다.

```ts
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input;
  }
  return padding + input;
}
```

그러나, 아래와 같은 에러를 마주할 수 있다. `array`타입과 `null`모두 `object`타입으로 자바스크립에서는 인지하기 때문이다. 그럴때는 “truthiness” checking를 하는게 좋다.

```ts
function printAll(strs: string | string[] | null) {
  if (typeof strs === "object") {
    for (const s of strs) {
      // error: Object is possibly 'null'.
      console.log(s);
    }
  } else if (typeof strs === "string") {
    console.log(strs);
  } else {
    // do nothing
  }
}
```

#### 2. Truthiness narrowing

위와 같은 예시에서 `null`을 걸러내기 위해서는 Truthiness 체크를 통해 걸러낼 수 있다.

```ts
// ex) strs의 truthiness를 확인
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    // 여기에다가 strc의 trutiness를 확인하도록 한다.
    for (const s of strs) {
      console.log(s);
    }
  } else if (typeof strs === "string") {
    // 앞에서 strs를 함께 거르면 empty string을 판단하지 못하는 경우 발생.
    console.log(strs);
  }
}
```

```ts
// ex) !를 사용하여 확인
function multiplyAll(
  values: number[] | undefined,
  factor: number
): number[] | undefined {
  if (!values) {
    return values;
  } else {
    return values.map((x) => x * factor);
  }
}
```

<`falsy` 한 값>

- 0
- NaN
- "" (the empty string)
- 0n (the bigint version of zero)
- null
- undefined

#### 3. Equality narrowing

타입스크립트에서는 또한 `switch`문과 `===`, `!==`, `==`, `!=`을 사용하여 동일성을 체크하여 타입을 좁힐 수 있다.

```ts
function example(x: string | number, y: string | boolean) {
  if (x === y) {
    // We can now call any 'string' method on 'x' or 'y'.
    x.toUpperCase();
    y.toLowerCase();
  } else {
    console.log(x); // x: string | number
    console.log(y); // y: string | boolean
  }
}
```

자바스크립트의 `==`, `!=`를 통한 느슨한 동등성(=looser equality)을 통해서도 올바르게 타입을 좁힐 수 있다.

```ts
interface Container {
  value: number | null | undefined;
}

function multiplyValue(container: Container, factor: number) {
  // Remove both 'null' and 'undefined' from the type.
  if (container.value != null) {
    console.log(container.value); //Container.value: number

    // Now we can safely multiply 'container.value'.
    container.value *= factor;
  }
}
```

#### 4. The `in` operator narrowing

자바스크립트의 `in`연산자를 이용해서, 객체의 프로퍼티의 이름을 확인하여 타입을 좁힐 수 있다.

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    return animal.swim();
  }

  return animal.fly();
}
```

같은 프로퍼티를 가지고 있는 경우는 두가지 경우 모두에 해당될 수 있다.

```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };
type Human = { swim?: () => void; fly?: () => void };

function move(animal: Fish | Bird | Human) {
  if ("swim" in animal) {
    animal; // animal: Fish | Human
  } else {
    animal; // animal: Bird | Human
  }
}
```

#### 5. `instanceof` narrowing

자바스크립트에는 다른 값이 해당 인스턴스의 값인지 아닌지 확인해주는 `instanceof` 연산자를 통해서 타입을 좁힐 수 있다.
(= instanceof 연산자는 생성자의 프로토타입 속성이 객체의 프로토타입 체인에 나타나는지 확인하기 위해 테스트합니다. 반환 값은 boolean 값입니다. 해당 동작은 `Symbol.hasInstance`로 사용자 정의할 수 있습니다.)

```ts
function logValue(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString()); // x: Date
  } else {
    console.log(x.toUpperCase()); // x: string
  }
}
```

#### 6. Assignments ( = 할당 )

변수에 할당할 때 TypeScript는 할당의 오른쪽을 보고 왼쪽을 적절하게 좁힙니다.

```ts
let x = Math.random() < 0.5 ? 10 : "hello world!"; // x: string | number

x = 1;
console.log(x); // let x: number;

x = "goodbye!";
console.log(x); //let x: string;
```

값을 할당할 때에 처음에 선언할때 지정한 타입과 다른 값이 할당되면 에러로 알려줍니다.

```ts
let x = Math.random() < 0.5 ? 10 : "hello world!"; // let x: string | number

x = 1;

console.log(x); // let x: number

x = true; // Error: Type 'boolean' is not assignable to type 'string | number'.

console.log(x); // let x: string | number
```

#### 7. Control flow analysis ( = 제어 흐름 분석 )

도달 가능성에 기반한 이러한 코드 분석을 제어 흐름 분석( = control flow analysis )이라고 합니다. 그리고, typescript는 이 흐름 분석을 사용하여 유형 가드 및 할당이 발생할 때 유형을 좁힙니다. 변수를 분석할 때 제어 흐름은 계속해서 분리되고 다시 병합될 수 있으며 해당 변수는 각 지점에서 다른 유형을 갖는 것으로 관찰될 수 있습니다.

```ts
function example() {
  let x: string | number | boolean;

  x = Math.random() < 0.5;

  console.log(x); // let x: boolean

  if (Math.random() < 0.5) {
    x = "hello";
    console.log(x); // let x: string
  } else {
    x = 100;
    console.log(x); // let x: number
  }

  return x; // let x: string | number
}
```

#### 8. Using type predicates

지금까지는 자바스크립에 구성으로 타입을 좁혔지만, 코드 전체에서 유형이 변경되는 ㅂ아식을 보다 직접적으로 제어하기를 원합니다. 사용자 정의 type guard 를 정의하려면 반환 유형이 **type predicate**의 함수를 정의하면 된다.

```ts
function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}
```

여기에서 `pet is Fish`가 type predicate에 해당한다. predicate는 `parameterName is Type`의 형식을 취합니다. 여기서 `parameterName`은 최근 함수의 서명에 parameter의 이름을 사용해야 합니다.

```ts
// Both calls to 'swim' and 'fly' are now okay.
let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

#### 9. Discriminated unions

지금까지는 단순한 타입을 좁히는것에 집중했지만 우리는 더욱 복잡한 것들을 다뤄야 할 때가 있다.

ex) bad

```ts
interface Shape {
  kind: "circle" | "square";
  radius?: number;
  sideLength?: number;
}

function getArea(shape: Shape) {
  if (shape.kind === "circle") {
    return Math.PI * shape.radius! ** 2;
    // Error: Object is possibly 'undefined'. 에 대처하기 위하여 !를 사용.
  }
}
```

ex) good

```ts
interface Circle {
  kind: "circle";
  radius: number;
}

interface Square {
  kind: "square";
  sideLength: number;
}

type Shape = Circle | Square;

function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2; // shape: Circle
    case "square":
      return shape.sideLength ** 2; // shape: Square
  }
}
```

제대로 된 정보로 Typescript와 소통하면 다른 방식으로 작성했을 JavaScript와 다르지 않은 안전한 유형의 TypeScript 코드를 작성할 수 있습니다. Discriminated unions를 사용하면 네트워크(클라이언트/서버 통신)를 통해 메시지를 보낼 때나 상태 관리 프레임워크에서 변형을 인코딩할 때와 같이 JavaScript에서 모든 종류의 메시징 체계를 나타내는 데 좋습니다.

#### 10. The never type

좁힐 때 모든 가능성을 제거하고 아무것도 남지 않은 지점까지 결합 옵션을 줄일 수 있습니다. 이러한 경우 TypeScript는 `never` 유형을 사용하여 존재해서는 안 되는 상태를 나타냅니다.

#### 11. Exhastiveness checking

`never`유형은 모든 유형에 할당할 수 있다. 그러나 `never`에 할당할 수 있는 유형은 없습니다. 즉, 타입 좁히기를 사용할 수 있고 `switch`문에서 철저한 검사를 수행하기 위해 절대 나타나지 않는 것에 의존할 수 있습니다.

```ts
type Shape = Circle | Square;

function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default:
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```

`switch`문에 default값에 never를 추가하면, 다뤄지지 않은 가능한 모든 케이스들을 발생시킨다.

예를들어, 새로운 `Shape`를 추가한다고 했을때 에러를 야기시킬수 있다.

```ts
interface Triangle {
  kind: "triangle";
  sideLength: number;
}

type Shape = Circle | Square | Triangle;

function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.sideLength ** 2;
    default: // Type 'Triangle' is not assignable to type 'never'.
      const _exhaustiveCheck: never = shape;
      return _exhaustiveCheck;
  }
}
```

---

## Typescript 관련 예상 면접 질문

### `alias`와 `interface`의 차이는?

- `alias`는 `extends` 또는 `implements` 될 수 없다. 하지만 `interface`로 표현할 수 없거나 유니온 또는 튜플을 사용해야 한다면 타입 `alias`를 사용하는게 유리하다.
- `interface`는 `extends`또는 `implements`될 수 있다. 상속을 통해 확장이 필요하다면 타입 `alias`보다는 `interface`가 유리하다.

---

### `unknown` vs `any` 차이는?

**< 등장 배경 >**
= `any`처럼 어떤 타입의 value든 할당할 수 있으면서 실제로 사용할 때는 개발자로 하여금 타입을 체킹하도록 만들 수 있는 타입이 필요했다. 그래서 조금 덜 수용적인 `unknown` 타입을 만들게 된 것이다.
= 사용자로부터 입력을 받거나 잘 알려지지 않은 외부 API를 사용하는 등 실제로 어떤 값이 올 지 모를 때, 어떤 값이든 할당할 수 있지만 정작 이후에 그 값을 사용할 때는 타입 체킹을 해서 안전하게 사용하게 하기 위해 쓸 수 있다.

**< 차이점 >**

- `any` 타입의 값은 어느 타입의 변수에도 할당될 수 있으나, `unknown` 타입의 값은 `any`와 `unknown` 타입을 제외한 타입의 변수에는 할당이 불가능하다.

ex)

```ts
let notSure: unknown;
notSure = 1;
notSure = "maybe a string instead";

// any type에는 unknown 타입 할당 가능
let anyType: any;
anyType = notSure;

// any, unknown 이외의 type에는 unknown 타입 할당 불가능
let numberType: number;
numberType = notSure; // compile error!
```

- `unknown`의 경우는, `any`와 다르게 에러를 뱉을 수 있다.

ex)

```ts
// any의 경우

let num: any = 99;
num.trim(); // 에러를 뱉어내지 않는다.

// unknown의 경우
let num: unknown = 99;
num.trim(); // Object is of type 'unknown'. 라는 에러를 뱉어낸다.

// unknown을 사용하며 타입가드를 사용하여 런타임 에러를 막는 경우
let num: unknown = 99;

if (typeof num === "string") {
  num.trim();
}

(num as string).trim();
```

ex)

```ts
// any의 경우

let foo: any = 10;

// All of these will throw errors, but TypeScript
// won't complain since `foo` has the type `any`.
foo.x.prop;
foo.y.prop;
foo.z.prop;
foo();
new foo();
upperCase(foo);
foo`hello world!`;

function upperCase(x: string) {
  return x.toUpperCase();
}
```

```ts
// unknown의 경우

let foo: unknown = 10;

// Since `foo` has type `unknown`, TypeScript
// errors on each of these usages.
foo.x.prop;
foo.y.prop;
foo.z.prop;
foo();
new foo();
upperCase(foo);
foo`hello world!`;

function upperCase(x: string) {
  return x.toUpperCase();
}
```

```ts
// unknown with type guard

let foo: unknown = 10;

function hasXYZ(obj: any): obj is { x: any; y: any; z: any } {
  return (
    !!obj && typeof obj === "object" && "x" in obj && "y" in obj && "z" in obj
  );
}

// Using a user-defined type guard...
if (hasXYZ(foo)) {
  // ...we're allowed to access certain properties again.
  foo.x.prop;
  foo.y.prop;
  foo.z.prop;
}

// We can also just convince TypeScript we know what we're doing
// by using a type assertion.
upperCase(foo as string);

function upperCase(x: string) {
  return x.toUpperCase();
}
```

[참고자료: [Typescript] unknown vs any type](https://roseline.oopy.io/dev/typescript-unknown-vs-any-type)
