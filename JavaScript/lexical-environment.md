# Lexical Environment

## 1. Lexical Environment 란?

Lexical Environment는 JavaScript 코드의 중첩된 구조에서 식별자가 어떤 변수, 어떤 함수를 가르키고 있는지 기록하는 정보에 대한 스펙입니다.

## 2. Lexical Environment 구성

Lexical Environment는 **Environment Record** 와 **outer** 로 구성되어 있습니다.

### Environment Record

Lexical Environment와 관련된 스코프에서 생성되는 식별자가 가르키는 함수, 변수에 대한 정보, **this**, **super** ...등에 대한 정보을 기록하고 있습니다.

### outer

해당 Lexical Environment의 바깥 Lexical Environment를 참조하고 있는데, 이는 외부 스코프의 식별자를 참조할 때 사용됩니다.(스코프 체인)

## 3. 클로저 (Closure)

클로저는 함수와 함수가 생성될 때 함수가 이를 감싸고 있는 환경을 기억하는 것입니다.

JavaScript에서 함수가 생성될 때, Lexical Environment에 대한 정보가 생성되는 함수의 `F.[[Environment]]`에 포함됩니다.

```js
function foo() {
  let c = 0;

  return function bar() {
    console.log(c ++);
  }
}

const bar = foo();
bar(); // 0
bar(); // 1
```

`foo` 가 실행되어 `bar` 함수를 반환할 때 Lexical Environment가 `bar`의 `F.[[Environment]]`에 포함됩니다.

`foo` 호출 이후 `bar`를 호출할 때, `foo`는 Execution Context Stack 스택에는 존재하지 않지만,
`bar`가 생성될 때 Lexical Environment를 기억하고 있고 그 안에는 `c`의 참조에 대한 정보가 있어 `c`에 접근할 수 있게 됩니다.
