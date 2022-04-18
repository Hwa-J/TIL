# JS 데이터 (자료형, Date Type)

## 원시형

1. 문자(String)
1. 숫자(Number)
1. 불린(Boolean)
1. null
1. underfined
1. 심볼(Symbol)
1. 큰정수(BigInt)

## 참조형

1. 배열(Array)
1. 객체(Object)
1. 함수(Function)

## 문자

따옴표로 묶여 있어야 함!

```js
'Happy';
'Happy'
`Happy`; // ${}보간을 쓸 떄만!
```

## 숫자

Not-A-Number - 숫자 데이터 / 숫자로 표기사 불가!
NaN

```js
1
123123
0.12341234
NaN
```

## 불린 (Boolearn)

```js
true
false
```

## null

(명시적) 없다
직접 없다고
'존재하지 않는', '비어있는', '알 수 없는' 값을 명시적으로 나타냄

## undefined

(암시적) 없다
'값이 할당되지 않는 상태'를 암시적으로 나타냄

## 심볼

유일한 식별자(ID) 데이터 이름을 만들 때 사용

```js
const s = Symbol('Hello world!'); //설명

const user = {
  name: 'Happy',
  [s]: 81,
};

console.log(user.name);
console.log(user[s]);
```

## BigInt

지수, 큰(Big) 정수(Integer)

## 배열

```js
const a = [1, '2', 3, {}, () => {}];
```

## 객체

```js
// Key: Value

const obj = {
  a: 'Apple'
  b: 'Banana'
  c: 'Cherry'
  b: 'Blueberry'
}

console.log(obj.b) // 점(Dot) 표기법
console.log(obj['b']) // 괄호(Bracket) 표기법
```

## 함수

```js
// 함수의 기본 형태
function happy() {
  // 명령1
  // 명령2
  // 명령3
  // 명령4
}
happy();
```

<br/>

# 형(Type)변환

```js
const a = 123
const b = '123'

console.log(a == b);
// true 반환
// (자동)형변환
```

==
동등 연산자

- 사용금지!!

=== 일치 연산자 (메모리 주소로 비교)

- 원시형은 똑같이 생기면 주소 같다.
- 자료형은 똑같이 생겨도 다를 수 있다.

<br/>

# Truethy & Falsy

## Falsy

```js
if (false)
if (null)
if (undefined)
if (0)
if (-0)
if (NaN)
if (0n)
if ('') //공백 문자(띄어쓰기 없음)
```

<br/>

# 자료형 확인

1. `typeof 데이터`
1. `데이터.constructor`
1. `Object.prototype.toString.call(데이터)`

null과 [ ]배열은 typeof으로 알아 낼 수 없다.

```js
console.log([].constructor === Array);
console.log(Array.isArray(''));

function checkType() {
  return Object.prototype.toString.call(data).slice(8, -1);
}
console.log(checkType([]));
console.log(checkType(null));
```

<br/>

# 변수

1. `const` (상수constant 변수)

- 유효범위: 블록 레벨
- 재할당: X
- 중복 선언: X
- 호이스팅(Hoisting): X
- 전역 등록: X

2. `let` (변수)

- 유효범위: 블록 레벨
- 재할당: O
- 중복 선언: X
- 호이스팅(Hoisting): X
- 전역 등록: X

3. `var` (사용금지)

- 유효범위: 함수 레벨
- 재할당: O
- 중복 선언: O
- 호이스팅(Hoisting): O
- 전역 등록: O

---

- 유효범위 (Scope)
- 재할당
- 중복 선언
- 호이스팅(Hoisting):  
  선언부를 밑에서 작성하고,
  위에서 호출했을 떄
  선언부를 유효범위 최상위로 끌어올리는 현상
- 전역(Global) 선언시 전역 객체(`window`)의 속성으로 등록

<br/>

# 함수

## 선언과 표현

1. 선언: 호이스팅 O
1. 표현: 호이스팅 X

```js
// 함수 선언
function abc() {}

// 함수 표현 (익명함수를 변수에 할당)
const abc = function () {};

const cde = {
  fn: function () {
    console.log('FN');
  },
};
```
