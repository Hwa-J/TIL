## 구조 분해 할당 (Destructuring assignment)
= 비구조화 할당

데이터의 구조를 분해해서 원하는 속성들만 꺼내 사용할 수 있는 개념  
- const, let 키워드로 구조 분해된 내용을 변수로 만들어 보간법으로 사용할 수 있다.
- 객체에서 점 표기법으로 속성값을 꺼내는 것과 동일  
`object.propertyKeyName`
- 배열에서 처럼 인덱싱 방법으로 속성값을 꺼낼 수 있다.  
`object['propertyKeyName']`

### 객체 데이터 구조분해 

```js
const user = {
  name: 'Heropy', 
  age: 85, 
  email: 'thesecon@gmail.com'
}
const { name, age, email, address } = user
// 구조 분해해서 원하는 속성들만 꺼내 변수로 선언하고, 객체 데이터 변수를 할당
// 구조 분해된 내용을 변수를 선언해 활용 가능 

console.log(`사용자의 이름은 ${name}입니다.`)
// 사용자의 이름은 Heropy입니다.
console.log(`${name}의 나이는 ${age}세 입니다.`)
// Heropy의 나이는 85세 입니다.
console.log(`${name}의 이메일 주소는 ${email}입니다.`)
// Heropy의 이메일 주소는 thesecon@gmail.com입니다.
console.log(address)
// undefined
```
- 속성의 기본값 설정
```js
const user = {
  name: 'Heropy', 
  age: 85, 
  email: 'thesecon@gmail.com'
}
const { name, age, address = 'Korea' } = user

console.log(`사용자의 이름은 ${name}입니다.`)
console.log(`${name}의 나이는 ${age}세 입니다.`)
console.log(`${name}의 이메일 주소는 ${user.email}입니다.`)
// Heropy의 이메일 주소는 thesecon@gmail.com입니다.
// 구조분해 변수에 속성 이름이 없어도 객체 변수에 점표기법으로 직접 출력
console.log(address)
// Korea
// 객체 데이터에 속성에 값이 없어도 기본값으로 설정한 값으로 출력
// (단, 객체 데이터에 속성값이 있으면 그 값으로 출력)
```
- 속성의 매개변수명 변경
```js
const user = {
  name: 'Heropy', 
  age: 85, 
  email: 'thesecon@gmail.com'
}
const { name: heropy, age, address = 'Korea' } = user
// 속성명(key)을 그대로 가져오지만 매개변수로 활용하는 이름을 변경하고 싶을 떄,
// :(콜론)기호로 변경할 수 있다.
// 속성명: 변경할 매개변수 명
// const heropy = name

console.log(`사용자의 이름은 ${heropy}입니다.`)
console.log(`${heropy}의 나이는 ${age}세 입니다.`)
console.log(`${heropy}의 이메일 주소는 ${user.email}입니다.`)
console.log(address)
// name이라는 매개변수는 사라짐
```

### 배열 데이터 구조분해
```js
const fruits = ['Apple', 'Banana', 'Cherry']
const [a, b, c, d] = fruits
// 배열은 index 순서대로 꺼내올 수 있다.
console.log(a, b, c, d)
// Apple Banana Cherry undefined
```
- Banana만 추출하기
```js
const fruits = ['Apple', 'Banana', 'Cherry']
const [, b] = fruits
// 배열은 순서대로 추출할 수 있어 매개변수르 넣지 않더라도 ,(쉼표)로 위치를 구분해 줘야 함
console.log(b)
// Banana
```
- Cherry 추출하기
```js
const fruits = ['Apple', 'Banana', 'Cherry']
const [, , b] = fruits
// 배열은 순서대로 추출할 수 있어 매개변수르 넣지 않더라도 ,(쉼표)로 위치를 구분해 줘야 함
console.log(b)
// Cherry
```

<br/>

## 전개 연산자 (Spread)
`...변수명`  
객체나 배열 데이터에서 쉼표로 구분된 각각의 데이터만 추출해 전개된다.  


```js
const fruits = ['Apple', 'Banana', 'Cherry']
console.log(fruits)
// ['Apple', 'Banana', 'Cherry']
console.log(...fruits)
// 'Apple', 'Banana', 'Cherry'
// console.log('Apple', 'Banana', 'Cherry')와 동작 같음

function toObject(a, b, c) {
  return {
    a: a,
    b: b,
    c: c
  }
}
console.log(toObject(...fruits))
// {a: 'Apple', b: 'Banana', c: 'Cherry'}
// console.log(toObject(fruits[0], fruits[1], fruits[2]))와 동작 같음
```

### 나머지 매개변수 (rest parameter)  
매개변수에도 `...`전개연산자 사용 가능 

```js
const fruits = ['Apple', 'Banana', 'Cherry', 'Orange']
console.log(fruits)
console.log(...fruits)

function toObject(a, b, ...c) {
  // 매개변수에도 ...전개연산자 사용 가능
  // ...c 매개변수가 'Cherry', 'Orange' 자리가 없는 인수 모두를 배열 형대로 순서대로 받는다
  return {
    a: a,
    b: b,
    c: c
  }
}
console.log(toObject(...fruits))
// {a: 'Apple', b: 'Banana', c: ['Cherry', 'Orange']}
```
- 객체데이터의 속성과 데이터의 값이 같으면(key = value) 축약 가능
```js
const fruits = ['Apple', 'Banana', 'Cherry', 'Orange']
console.log(fruits)
console.log(...fruits)

function toObject(a, b, ...c) {

  return {
    a,
    b,
    c
  }
}
console.log(toObject(...fruits))
// {a: 'Apple', b: 'Banana', c: ['Cherry', 'Orange']}
```
- 화살표 함수로 축약
```js
const fruits = ['Apple', 'Banana', 'Cherry', 'Orange']
console.log(fruits)
console.log(...fruits)

const toObject = (a, b, ...c) => ({a, b, c})
console.log(toObject(...fruits))
// {a: 'Apple', b: 'Banana', c: ['Cherry', 'Orange']}
```

<br/>

## 데이터의 불변성 (Immutability)

### 원시 데이터: String, Number, Boolean, undefined, null  
  - 생긴 것이 같으면 같은 데이터이다. (데이터 자체가 변하지 않는 성질이기 때문)  
  - **기존 메모리에 없는** 원시 데이터를 생성할 떄만 **새로운 메모리**에 추가함,  
  **기존 메모리에 있는** 원시 데이터는 **꺼내 씀**    
  <br/>

  
### 참조형 데이터: Object, Array, Function  
  - 생긴 것이 같아도 같은 데이터가 아닐 수도 있다.  
  - 참조형 데이터를 **새로 생성**할 떄 마다 **새로운 메모리**에 추가
  - 참조형 데이터를 **할당** 하는 것은 값을 복사하는 것이 아닌 **메모리의 참조 주소만 연결**시키는 것  
  - 메모리 주소가 연결되어 있으면 어느 한쪽에서 객체 데이터에서 수정하든 둘 다 수정된다.  
  - 메모리 주소만 옮길 의도라면 상관없지만  
  기존 데이터를 할당받고 따로 구분해 관리하고 싶다면 복사라는 개념을 사용해야 함

```js
let a = { k : 1 }
let b = { k : 1 }
console.log(a, b, a === b) // {k: 1} {k: 1} false
a.k = 7
b = a // 메모리 참조주소 연결
console.log(a, b, a === b) // {k: 7} {k: 7} true
a.k = 2
console.log(a, b, a === b)    // {k: 2} {k: 2} true
                              // 의도하지 않게 b 속성의 값도 함께 바뀜 (같은 메모리 주소)
let c = b // 메모리 참조주소 연결
console.log(a, b, c, a === c) // {k: 2} {k: 2} {k: 2} true
a.k = 9
console.log(a, b, c, a === c) // {k: 9} {k: 9} {k: 9} true
                              // 의도하지 않게 b, c 속성의 값도 함께 바뀜 (같은 메모리 주소)
```

<br/>

## 얕은 복사와 깊은 복사

### 얕은 복사 (Shallow copy)
- 겉 표면만 복사
- 참조형 데이터(객체, 배열, 함수)를 복사할 때 그 안에 또 다른 참조형 데이터가 없다는 전제 하에 사용 권장


```js
const user = {
  name: 'Heropy', 
  age: 85, 
  emails: ['thesecon@gmail.com']
}
const copyUser = user
console.log(copyUser === user)  // true

user.age = 22
console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com']}
console.log('copyUser', copyUser)
// user와 copyUser의 메모리 주소가 연결되어 있어 어느 한쪽에서 객체 데이터에서 수정하든 둘 다 수정된다.
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com']}
```
- 복사 방법 1 (assign메소드)
```js
const user = {
  name: 'Heropy', 
  age: 85, 
  emails: ['thesecon@gmail.com']
}
const copyUser = Object.assign({}, user)  // {}리터럴 방식으로 새로운 메모리에 추가 (assign메소드 복사 개념)
console.log(copyUser === user)  // false

user.age = 22
console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com']}
console.log('copyUser', copyUser)
// user와 copyUser의 메모리 주소가 달라 user의 속성이 바뀌어도 영향X
// {name: 'Heropy', age: 85, emails: ['thesecon@gmail.com']}
```
- 복사 방법 2 (...전개연산자)
```js
const user = {
  name: 'Heropy', 
  age: 85, 
  emails: ['thesecon@gmail.com']
}
const copyUser = {...user}  // {}리터럴 방식으로 새로운 메모리에 추가 (...전개연산자 복사 개념)
console.log(copyUser === user)  // false

user.age = 22
console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com']}
console.log('copyUser', copyUser)
// user와 copyUser의 메모리 주소가 달라 user의 속성이 바뀌어도 영향X
// {name: 'Heropy', age: 85, emails: ['thesecon@gmail.com']}
```
- 얕은 복사의 문제 (참조형 데이터 속에 존재하는 또다른 참조형 데이터는 복사하지 못함(복사 전 메모리 참조 주소 연결))
```js
user.email.push('neo@zillinks.com')
console.log(user.emails === copyUser.emails)  // true
// user객체 데이터만 복사한 것으로 그 속의 emails속성의 배열 데이터는 같은 메모리 주소를 공유하고 있다.

console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com, neo@zillinks.com']}
console.log('copyUser', copyUser)
// {name: 'Heropy', age: 85, emails: ['thesecon@gmail.com, neo@zillinks.com']}
```


### 깊은 복사 (Deep copy)
내부의 모든 참조 관계까지 새로운 메모리로 복사
- 참조형 데이터(객체, 배열, 함수)를 복사할 때 그 안에 또 다른 참조형 데이터가 있다면 깊은 복사를 고려하여 사용

- 직접 코드로 작성하기엔 복잡해서, JS 패키지 중 하나인 lodashdml  `_.cloneDeep()`메소드 사용
```js
import _ from 'lodash'

const user = {
  name: 'Heropy', 
  age: 85, 
  emails: ['thesecon@gmail.com']
}
const copyUser = _.cloneDeep(user)
console.log(copyUser === user)  // false

user.age = 22
console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com']}
console.log('copyUser', copyUser)
// {name: 'Heropy', age: 85, emails: ['thesecon@gmail.com']}


user.email.push('neo@zillinks.com')
console.log(user.emails === copyUser.emails)  // false

console.log('user', user)
// {name: 'Heropy', age: 22, emails: ['thesecon@gmail.com, neo@zillinks.com']}
console.log('copyUser', copyUser)
// {name: 'Heropy', age: 85, emails: ['thesecon@gmail.com}
```