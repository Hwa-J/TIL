# JS 데이터

## 객체

`Object`  
주어진 값에 대한 객체 래퍼를 생성하는 생성자

JavaScript의 거의 모든 객체는 Object의 인스턴스


<br/>

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(numbers[1])
console.log(fruits[2])
```

<br/>

### Object.Methods

- 정적(Static) 메소드  
리터럴 방식으로 생성한 데이터에 직접적으로 메소드 사용을 못함  
전역객체인 Object에 직접적으로 사용  

<br/>


#### `.assign()` 메소드

열거할 수 있는 하나 이상의 출처 객체로부터 대상 객체로 속성을 복사할 때 사용합니다.  
출처 객체가 복사된 대상객체가 반환
- 원본(대상 객체) 수정됨 주의! 

`Object.assign(대상객체, 복사 출처 객체1, 출처객체2, 3...)`

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// { a: 1, b: 4, c: 5 }

console.log(returnedTarget);
// { a: 1, b: 4, c: 5 }
```
```js
const userAge = {
  // key: value
  name: 'Heropy'
  age: 85
}
const userEmail = {
  name: 'Heropy',
  email: 'thesecon@gmail.com'
}

const target = Object.assign(userAge, userEmail)
console.log(target) 
//{name: "Heropy", age: 85, email: "thesecon@gmail.com"}
console.log(userAge) 
//{name: "Heropy", age: 85, email: "thesecon@gmail.com"}
console.log(target === userAge) // true (같은 메모리 공유)

const a = { K: 123 }
const b = { K: 123 }
console.log(a === b) // false (똑같이 생겼다고 일치X, 다른 메모리)
```

- 대상 객체 수정 없이 사용하기 (새로운 객체 생성)  
대상 객체의 자리에 {} 빈 리터럴 생성자를 넣는다.
```js
const userAge = {
  // key: value
  name: 'Heropy'
  age: 85
}
const userEmail = {
  name: 'Heropy',
  email: 'thesecon@gmail.com'
}

const target = Object.assign({}, userAge, userEmail)
console.log(target) 
//{name: "Heropy", age: 85, email: "thesecon@gmail.com"}
console.log(userAge) 
//{name: "Heropy", age: 85}
console.log(target === userAge) // false (다른 메모리)

const a = { K: 123 }
const b = { K: 123 }
console.log(a === b) // false (똑같이 생겼다고 일치X, 다른 메모리)
```
<br/>


#### `.keys()` 메소드

대상 객체의 속성(property, key)값을 추출해 배열 데이터로 반환

```js
const user = {
  // key: value
  name: 'Heropy'
  age: 85
  email: 'thesecon@gmail.com'
}

const keys = Object.keys(user)
console.log(keys)
// ["name", "age", "email"]

console.log(user['email']) // 객체 데이터 인덱싱
// thesecon@gmail.com

const values = key.map(key => user[key])
console.log(values)
// ["Heropy", 85, "email"]
```