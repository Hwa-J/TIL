# 함수

소괄호를 열고 닫기 전에는
호출하기 전까지 하나의 데이터로 볼 수 있다.

<br/>

## new Function()

생성자 함수 호출로 함수를 만드는 법!
근데 자주 안씀.

```js
const sum = new Function('a', 'b', 'console.log(a + b)')
sum(2, 4)

// new: 생성
// Function: 함수 클래스
```

<br/>

## 반환과 종료

`return`  
`undefined`  
  
`return` 키워드를 사용하면 데이터를 반환하고 함수 종료!  
return 키워드를 사용하지 않았을 떄 함수를 호출하면 undefined 데이터가 반환된다. 

<br/>

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

<br/>

## 매개변수

매개변수 이름은 내가 맘대로 지정할 수 있다.
그래도 유지보수 위해 명시적으로 작성하는 것을 권장한다.

```js
function callFn (callback) {
  callback()
}

// callback이라는 (매개)변수가 선언(만들어진 것)
// 코드 아래에 callback함수가 호출되었는데, 
// 위레서 let이나 const로 따로 변수가 선언이 되어진 것을 보지 못했다면 (매개)변수로 선언되어진 것이다.
```

<br/>

### 매개변수 기본값


```js
function sum (a, b) {
  return a + b
}
console.log(sum(2, 4))  // 6
console.log(sum(5, 7))  // 12
console.log(sum(4))     // NaN = 4 + undefined
console.log(sum())      // NaN = undefined + undefined
```

```js
// 기본값 지정

function sum (a = 1, b = 3) {
  return a + b
}
console.log(sum(2, 4))  // 6
console.log(sum(5, 7))  // 12
console.log(sum(4))     // 7
console.log(sum())      // 4
```

<br/>

### ※ 구조 분해 할당(Destructuring assigment) (중요‼️)

```js
const user = {
  name: 'Heropy',
  age: 85,
}

function getName(user) {  
  const name = user.name
  const age = user.age

  return [name, age]
}
console.log(getName(user))  // ['Heropy', 85]
```

```js
//구조분해 할당 사용

const user = {
  // key: velue
  name: 'Heropy',
  age: 85,
}

function getName({ name, age }) {  // 매개변수를 key이름 그대로 지정
  return [name, age]
}
console.log(getName(user))  // ['Heropy', 85]
```

```js
// 잘못된 방법

const user = {
  name: 'Heropy',
  age: 85,
}

function getName({ email, age }) { // key가 없음
  return [email, age]
}
console.log(getName(user))  // [undefined, 85]


// 해결 1

const user = {
  name: 'Heropy',
  age: 85,
}

function getName({ name, age }) {
  const email = name;
  return [email, age]
}
console.log(getName(user))  // ['Heropy', 85]


// 해결 2

const user = {
  name: 'Heropy',
  age: 85,
}

function getName({ name: email, age }) {
  return [email, age]
}
console.log(getName(user))  // ['Heropy', 85]


// 해결 3

const user = {
  name: 'Heropy',
  age: 85,
}

function getName({ name, age, email = 'these@mail.com' }) { // = 기호로 기본값 지정
  return [name, age, email]
}
console.log(getName(user)) ['Heropy', 85, 'these@mail.com']
```

<br/>

### ※ 나머지 매개변수(Reset parameter) (중요‼️)

  
`...`  
  전개 연산자 (spread operator)  

`...rest`  
  나머지 매개변수(rest parameter)  
- 인수들을 배열 데이터 타입으로 받음  
- 매개변수 명은 맘대로 지을 수 있지만 통상적으로 rest를 많이 사용한다. 

```js
function sum(a, b, c) {
  return a + b + c
}

console.log(sum(1, 2, 3, 4))    // 6
```
```js
function sum(...rest) {
  console.log(rest)             // [1, 2, 3, 4]
}                               // rest(나머지 매개변수)는 [배열] 데이터를 받는다.

console.log(sum(1, 2, 3, 4))    // undefined
```

<br/>

보너스) 배열 데이터 계산하기
```js
function sum(a, b, ...rest) {
  console.log(rest)             // [1, 2, 3, 4, 5, 6, 7, 8, 9]

  return rest.reduce(function (acc, cur) {
    return acc + cur
  })
}

console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9))    // 45
```
```js
// 화살표 함수
function sum(...rest) {

  return rest.reduce((acc, cur) => acc +cur)
}

console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9))    // 45
```

<br/>

보너스) 전개 연산자를 이용한 얕은 복사(Shallow Copy)
```js
const user = {
  name: 'Heropy',
  age: 85
}
const email = {
  email: 'thesecon@gmail.com'
}


// assign 함수 사용
const res = Object.assign({}, user, email)
console.log(res)  // {name: 'Heropy', age: 85, email: 'thesecon@gmail.com'}


// 전개 연산자 사용
const res = {
  ...user,
  ...email
}
console.log(res)  // {name: 'Heropy', age: 85, email: 'thesecon@gmail.com'}
```
```js
const a = [1, 2, 3]
const b = [3, 4, 5]


// concat 함수 사용
const res = a.concat(b)
console.log(res)    // [1, 2, 3, 3, 4, 5]


// 전개 연산자 사용
const res = [...a, ...b]
console.log(res)    // [1, 2, 3, 3, 4, 5]
```




<br/>

### `arguments` 객체  
- 암시적인 변수 데이터
- 객체 데이터 형태를 통해서 유사배열 객체로 저장 됨
- arguments 대신 전개 연산자를 사용하는 나머지 매개변수를 사용 권장!!


```js
function sum() {
  console.log(arguments)  // [1, 2, 3, 4, 5, 6, 7, 8, 9]
                          // 배열처럼 보이지만 배열이 아님(유사 배열 객체)
  return rest.reduce(function (acc, cur) {
    return acc + cur
  })
}
console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9)) 
//유사 배열 객체(Array-like object)은 reduce 못 써서 에러 뜸
```


```js
//에러 해결

function sum() {
  console.log(arguments)  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

  let res = 0
  for (const item of arguments) {
    res += item
  }
  return res
}
console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9))    // 45

// 명시적인 나머지 매개변수를 사용

function sum(...rest) {
  let res = 0
  for (const item of rest) {
    res += item
  }
  return res
}
console.log(sum(1, 2, 3, 4, 5, 6, 7, 8, 9))    // 45
```


## IIFE

Immediately-Invoked Function Expression  
즉시 실행 함수 (표현식)
- 익명함수를 실행할 때 사용
- 익명함수를 ()소괄호로 묶고 ()소괄호로 호출(실행)

```
;(익명함수)()
;((익명함수)())
```

```js
(function () {
  console.log(123)
})()

(function () {
  console.log(123)
}())
```
```js
console.log(456)

// 직전 명령에 ;이 없으면 에러가 남
// 그래서 즉시 실행 함수 앞에 ;를 붙임
;(function () {
  console.log(123)
})()
```


## 호이스팅


선언부가 위로 끌어 올려지는 현상  
- 기명 함수 선언에서 발생  
- 중요도에 따라 코드를 작성할 때 유용 (중요도 낮은 기명 함수를 일부러 밑에 작성)


```js
abc()

function abc() {
  console.log(123)
}
```

## 콜백

콜백 함수(Callback function) => 콜백  

함수의 인수(데이터)로 사용되는 함수

```js
function abc(callback) {
  callback()
}

abc(function () {
  console.log('ABC')
})
```

```js
// setTimeout(함수, 지연시간ms)

function abc() {
  console.log('ABC')
}

setTimeout(abc(), 1000)    // setTimeout(undefined, 1000)
setTimeout(abc, 1000)      // 1초 뒤에 abc함수 실행


clearTimeout(abc)  // setTimeout의 실행 함수를 멈추는 함수 (실행 함수의 이름을 알아야 함)



// 번외) setTimeout 함수만 사용 할땐 익명 함수로 많이 사용
setTimeout(function () {
  console.log('ABC')
}, 1000)

```

```js
function sum(a, b, cb) {     // cb = callback 약어
  return cb(a, b)
}

const res = sum(2, 5, function(a, b) {
  return a + b
})

console.log(res)    // 7
```

```js
function sum(a, b, cb) {
  setTimeout(function () {
    cb(a + b)
  }, 1000)
}

sum(2, 5, function (res) {
  console.log(res)    // 7 (1초 뒤에 출력됨)
})
```