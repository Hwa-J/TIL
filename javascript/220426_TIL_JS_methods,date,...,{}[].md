#### `.reduce()` 메소드
콜백이 실행될 때마다 **누적된 값**을 **다음 콜백 실행 값**으로 넘긴다.
- 중간에 중지 못함
```js
// arr.reduce((accumulator, currentValue) => {}, 초기값)

arr.reduce((누적값, 현재값) => {}, 초기값)
```
```js
// 배열의 모든 값 더하기
const arr = [1, 2, 3, 4]

// for문
let sum = 0
for (let i =0; i < acc.length; i += 1) {
  sum += arr[i]
}

// .forEach() 메소드
let sum = 0
arr.forEach(item => {
  sum += item
})

// .reduce() 메소드
const sum = arr.reduce((acc, cur) => {
  return acc + cur
}, 0)
// 1번쨰 실행될때 초기값 0이 acc의 인수. 첫째 배열값은 cur의 인수로 들어감
// 2번째 실행될 떄 1번쨰 반환값이 acc의 인수로 들어감, 둘째 배열값은 cur의 인수로 들어감
// 3번째 실행될 떄 2번쨰 반환값이 acc의 인수로 들어감, 셋째 배열값은 cur의 인수로 들어감
// ...
```

#### `.reverse()` 메소드
배열의 순서를 반전(거꾸로 뒤집기)시킨다.
- 원본 수정됨 주의!
```js
const arr = [1, 2, 3, 4, 5]

console.log(arr.reverse())
// [5, 4, 3, 2, 1]
console.log(arr)
// [5, 4, 3, 2, 1]

```
#### `.slice()` 메소드
첫번째 인수부터 두번째 인수의 직전까지 아이템을 남기고 삭제한다.
```js
const arr = [1, 2, 3, 4, 5]
console.log(arr.slice(0, 3)) // [1, 2, 3]
```

#### `.some()` 메소드
콜백 함수를 배열의 요소 중 **최소 하나라도 만족**하는지 판별
```js
const arr = [1, 2, 3, 4, 5]
console.log(
  arr.some(item => item === 1)
)
// true
```
#### `.splice()` 메소드
기본 배열이 삭제, 교체, 추가 가능
```js
const arr = ['a', 'b', 'c', 'd']
// .splice(인덱스, 삭제개수, 추가데이터)
console.log(
  arr.splice(2, 2, 'x')  // ['c', 'd']
)
console.log(arr) // ['a', 'b', 'x']
```
<br/>

### Object (객체)

#### Object`.assign()` 정적 메소드
첫번째 인수에 들어가는 기존 객체 안에 다음 인수의 객체의 내용을 복붙
```js
const userA = {
  name: 'Heropy',
  age: 85
}
const userB = {}

Object.assign(userB, userA)

console.log(userB)
// {name: 'Heropy', age: 85}
```
```js
const res = data.reduce((acc, name) => {
  return Object.assign(acc, {
  [name] () {
    console.log(123)
    }
  })
}, {})
```
```js
const userA = {
  name: 'Heropy',
  age: 85
}
const userC = {
  name: 'Amy',
  isValid: true
}
const userB = {}

Object.assign(userB, userA, userC)
// userB 대상, userA userC 객체
console.log(userB)
// {age: 85, name: 'Amy', isValid: true}
// 나중에 들어온 userC 객체의 name속성 값이 최종 덮어버림
```

```js
const userA = {
  name: 'Heropy',
  age: 85
}
const userC = {
  name: 'Amy',
  isValid: true
}
const userB = {
  name: 'Neo',
}

const res = Object.assign({}, userB, userA, userC)
// {}대상, userA userB userC 객체
console.log(res)
// {age: 85, name: 'Amy', isValid: true}
// 나중에 들어온 userC 객체의 name속성 값이 최종 덮어버림
```

#### Object`.entries()` 메소드  
객체 데이터의 `key: value` 형태를 배열로 전환시키고  
전환 시킨 배열을 다시 배열로 묶어 2차원 배열로 반환한다.
- 응용
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const res = Object.entries(userA)
console.log(res)

for (const item of res) {
  console.log(item[0]) // key
  console.log(item[1]) // value
}
```
- 축약
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}

for (const item of Object.entries(userA)) {
  console.log(item[0]) // key
  console.log(item[1]) // value
}
```

#### Object`.keys()` 메소드
객체의 각 속성(key)들을 모아 배열로 반환
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const res = Object.keys(userA)
console.log(res)
// ['name', 'age', 'isValid']
```
- 각 key의 값 출력 
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const res = Object.keys(userA)
res.forEach(item => {
  console.log(userA[item])
})
// Heropy
// 85
// true
```
- 축약 (메소드 체이닝)
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
Object.keys(userA).forEach(item => {
  console.log(userA[item])
})
// Heropy
// 85
// true
```
- 응용 (상태 관리)
```js
const state = {
  name: '',
  age: '',
  isValid: false
}
const mutations = {
  setState(payload) {
    Object.keys(payload).forEach(key => {
      state[key] = payload[key]
    })
  }
}

mutations.setState({
  name: 'Heropy',
  age: 85
})
```

#### Object`.values()` 메소드
객체의 각 속성의 값들을 모아 배열로 반환
```js
const userA = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const res = Object.values(userA)
console.log(res) // ['Heropy', 85, true]
```

# 날짜와 시간

## new Date() 생성자 함수

```js
const res = new Date()
console.loog(res.getFullYear())
console.loog(res.getMonth() + 1)
console.loog(res.getDate())
console.loog(res.getDay())
console.loog(res.getHours())
console.loog(res.getMinutes())
console.loog(res.getSeconds())
```
```js
const currentDay = ''
switch (res.getDay()) {
  case 0:
    currentDay = '일요일'
    break
  case 1:
    ...
}
```
## Date.now() 정적 메소드
```js
// Date.now() 정적 메소드
console.log(Date.now())
// 1970.01.01 00:00:00부터 현재 까지 경과시간을 ms단위로 반환
```
```js
// 실행 경과 시간을 알 수 있음

const now = Date.now()

for (let i =0; i < 1000; i += 1) {
  console.log('')
}

console.log(Date.now() - now)
```
- moment.js (무거움, 기능 많음)  
https://momentjs.com/  
https://cdnjs.com/libraries/moment.js
```js
moment().format('YYYY년 MM월 DD일 HH:mm:ss ddd')
```
- Day.js (가벼움)  
https://day.js.org/
```js
moment().format(YYYY년 MM월 DD일 )
```

# 전개 연산자
...가 객체나 배열의 괄호를 삭제하고 내부 값을 펼쳐낸다.
- 배열
```js
const a = [1, 2, 3]
const b = [4, 5, 6]

const c = a.concat(b)
console.log(c) // [1, 2, 3, 4, 5, 6]

const d = [...a, ...b]
// [...[1, 2, 3], ...[4, 5, 6]]
console.log(d)
// [1, 2, 3, 4, 5, 6]
```
- 객체
```js
const a = {
  x: 1,
  y: 2
}

const b = {
  y: 3,
  z: 4
}

const c = Object.assign({}, a, b)
console.log(c)
// {x: 1, y: 3, z: 4}

const d = {
  ...a,
  ...b
} 
// {...{x: 1, y: 2}, ...{y: 3, z: 4}}

console.log(d)
// {x: 1, y: 3, z: 4}
```
```js
const a = [1, 2, 3]

function fn(x, y, z) {
  console.log(x, y, z)
}
fn(...a)
// fn(1, 2, 3)
// 1 2 3
```
```js
const a = [1, 2, 3]

function fn(x, ...rest) {
  console.log(x, rest)
}
fn(...a)
// 1 [2, 3]
```

# 구조 분해 할당
## 배열 & 객체에서 활용
특정 데이터만 뽑아서 사용

### 객체
```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const { isValid } = user
console.log(isValid) // true
```
- 기본값 지정 가능
```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const { email = 'thesecon@gmail.com' } = user
console.log(email) // thesecon@gmail.com
```
- 변수명 대체 사용
```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const { email: e = 'thesecon@gmail.com' } = user
console.log(e) // thesecon@gmail.com
```
- 값을 여러개 사용할때 유용 
```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
// const e = user.name
// const a = user.age
// const i = user.isValid
const { 
  name: e, 
  age: a, 
  isvalid: i,
  email: x = 'the'
} = user
console.log(e, a, i, x) // Heropy 85 true the
```
- 전개 연산자 활용
```js
const user = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
const { 
  name: e, 
  ...rest
} = user
console.log(e, rest) // Heropy {age: 85, isValid: true}
```

### 배열
key가 없어 순서대로만 반환 가능
```js
const arr = [1, 2, 3]
const [x, y, z] = arr

console.log(x, y, z) // 1 2 3
```
- 3 하나만 출력 (몇개 안되는 배열 데이터만 사용)
```js
const arr = [1, 2, 3]
const [,, z] = arr

console.log(z) // 3
```
- 기본값 지정
```js
const arr = [1, 2, 3, 7]
const [,x,,a = 99] = arr

console.log(a) // 7
```
- 객체의 key: value 원본 데이터만 가져오기
```js
const user = {
  name: 'Heropy',
  age: 85
}
for (const [k, v] of Object.entrise(user)) {
  console.log(k, v)
}
```

- 맞교환
```js
let a = 1
let b = 3

// const backup = a
// a = b
// b = backup
;[b, a] = [a, b]

console.log(a) // 3
console.log(b) // 1
```
- 전개 연산자 (나머지 매개변수)
```js
const arr = [1, 2, 3, 4, 5, 6, 7, 8]
const [x, y, ...rest] = arr

console.log(x, y, rest}
// 1 2 [3, 4, 5, 6, 7, 8]
```