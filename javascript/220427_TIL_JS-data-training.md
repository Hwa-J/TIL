# JS 데이터 실습

## 가져오기(import), 내보내기(export)

### `import`  
외부에 있는 JS파일을 **가져올** 수 있는 통로를 만들어 주는 키워드   

### `export default`  
특정한 JS파일을 **외부로 내보낼** 수 있도록 **기본 통로**를 만들어 주는 키워드  
- 이름을 따로 지정하지 않아도 됨 (기본 통로)  
- 가져올 때(`import`)에도 언제든지 다른 이름으로 지정해도 전혀 문제X  
- 기본 통로에서는 (하나의 JS파일에서) 하나의 데이터(기능)만 내보낼 수 있다.


```js
// main.js

import _ from 'lodash' // From `node-modules`!
// from 뒤에 문자 데이터로 사용할 패키지 이름만 명시(별도 경로X)
// lodash패키지의 이름은 보통 _로 설정

import getType from './getType' // getType.js
import getRandom from './getRandom' // getRandom.js

console.log(_.camelCase('the hello world')) // theHelloWorld
console.log(getType([1, 2, 3])) // Array
console.log(getRandom(), getRandom()) // 랜덤숫자 2개
```

```js
// getType.js

export default function getType(data) {
  return Object.prototype.toString.call(data).slice(8, -1)
}
// 축약(이름 생략) 
export default function (data) {
  return Object.prototype.toString.call(data).slice(8, -1)
}


// main.js

import checkType from './getType' // getType.js
// 불러올 이름을 원하는 이름으로 변경 가능
console.log(getType([1, 2, 3])) // Array
```
```js
// getRandom.js

export default function random() {
  return Math.floor(Math.random() * 10)
}

// 축약(이름 생략) 
export default function () {
  return Math.floor(Math.random() * 10)
}


// main.js

import random from './getRandom' // getRandom.js
console.log(getRandom(), getRandom()) // 랜덤숫자 2개
```
- 한 파일에 여러기능 쓸 경우 에러
```js
export default function (data) {
  return Object.prototype.toString.call(data).slice(8, -1)
}
export default 123

// Only one default export allowed per module. 에러 발생
```

### `export`  
특정한 JS파일을 **외부로 내보낼** 수 있도록 **이름이 정해진 통로**를 만들어 주는 키워드  
- 이름을 꼭 지정해야 하는 통로  
- 이름이 지정된 통로에서 가져올 데이터는 {중괄호}로 이름을 묶어서 가져와(`import`)야 한다.  
- 이름이 지정된 통로에서는 데이터(기능) 개수 상관없이 내보낼 수 있다.  
(이름이 지정된 내보내기와 기본 내보내기 같이 사용 가능)

번외)
- 이름이 지정된 통로에서 가져온(`import`) 데이터의 명칭을 `as`를 통해 변경 가능  
(객체 분해 구조의 :(콜론)과 같은 역할)
- 와일드 카드(Wildcard Character, `*`)  
**여러 내용을 한꺼번에 지정할 목적**으로 사용하는 기호를 가리킨다. 

```js
// getRandom.js

export function random() {
  return Math.floor(Math.random() * 10)
}


// main.js

import { random } from './getRandom' // getRandom.js
// 이름이 지정된 통로로 받은 데이터는 {중괄호}로 묶어서 사용해야한다.

console.log(getRandom(), getRandom()) // 랜덤숫자 2개
```
- 여러개 내보내기
```js
// getRandom.js

export function random() {
  return Math.floor(Math.random() * 10)
}
export const user = {
  name: 'HEROPY',
  age: 85
}


// main.js

import { random, user } from './getRandom' // getRandom.js
// 이름이 지정된 통로로 받은 데이터는 {중괄호}로 묶어서 사용해야한다.

console.log(getRandom(), getRandom()) // 랜덤숫자 2개
console.log(user) // {name: 'HEROPY', age: 85}
```
- 이름이 지정된 통로에서 가져온 **데이터의 명칭을 `as`를 통해 바꾸기**
```js
// getRandom.js

export function random() {
  return Math.floor(Math.random() * 10)
}
export const user = {
  name: 'HEROPY',
  age: 85
}


// main.js

import { random, user as heropy } from './getRandom' // getRandom.js


console.log(getRandom(), getRandom()) // 랜덤숫자 2개
console.log(heropy) // {name: 'HEROPY', age: 85}
```
- 이름이 지정된 통로에서 **데이터 전체(*) 가져오기**
```js
// getRandom.js

export function random() {
  return Math.floor(Math.random() * 10)
}
export const user = {
  name: 'HEROPY',
  age: 85
}
export default 123


// main.js

import * as naeMam from './getRandom' // getRandom.js
// naeMam 명칭은 내가 원하는대로 지정 가능

console.log(neaMam) 
// {user: {name: 'HEROPY', age: 85}, random: function random() {return Math.floor(Math.random() * 10), 123}
```

<dr/>

## Lodash 사용법

### _.uniqBy() 메소드
`_.uniqBy(배열 데이터명, '고유값으로 설정할 속성명')`  
대상 배열에서 지정한 속성 이름으로 고유한 값만 정리(중복값 삭제)해서 반환함  
- 이미 중복이 발생한 배열에 사용
```js
import _ from 'lodash'

const usersA = [
  { userId: '1', name: 'HEROPY' },
  { userId: '2', name: 'Neo' }
]
const usersB = [
  { userId: '1', name: 'HEROPY' },
  { userId: '3', name: 'Amy' }
]
const usersC = usersA.concat(usersB)
console.log(usersC)
/* [{ userId: '1', name: 'HEROPY' }, 
    { userId: '2', name: 'Neo' }, 
    { userId: '1', name: 'HEROPY' }, 
    { userId: '3', name: 'Amy' }] */
console.log(_.uniqBy(usersC, 'userId'))
/* [{ userId: '1', name: 'HEROPY' }, 
    { userId: '2', name: 'Neo' }, 
    { userId: '3', name: 'Amy' }] */
```

### _.unionBy() 메소드
`_.unionBy(배열 데이터명1, 배열 데이터명2, ..., '고유값으로 설정할 속성명')`  
배열을 병합하면서 지정한 속성 이름으로 고유한 값만 정리(중복값 삭제)해서 반환
- 중복이 발생할 수 있는 배열을 합치기 전에 사용
```js
import _ from 'lodash'

const usersA = [
  { userId: '1', name: 'HEROPY' },
  { userId: '2', name: 'Neo' }
]
const usersB = [
  { userId: '1', name: 'HEROPY' },
  { userId: '3', name: 'Amy' }
]
const usersD = _.unionBy(usersA, usersB, 'userId')
console.log(usersD)
/* [{ userId: '1', name: 'HEROPY' }, 
    { userId: '2', name: 'Neo' }, 
    { userId: '3', name: 'Amy' }] */
```

### _.find() 메소드
`_.find(배열 데이터명, 찾을 데이터 조건)`  
내용이 많은 배열 데이터 안에서 특정한 객체 데이터를 찾을 때 유용
```js
const users = [
  { userId: '1', name: 'HEROPY' },
  { userId: '2', name: 'Neo' },
  { userId: '3', name: 'Amy' }
  { userId: '4', name: 'Evan' }
  { userId: '5', name: 'Lewis' }
]
const foundUser = _.find(users, { name: 'Amy' })
console.log(foundUser)
// { userId: '3', name: 'Amy' }
```

### _.findIndex() 메소드
`_.findIndex(배열 데이터명, 찾을 데이터 조건)`  
내용이 많은 배열 데이터 안에서 특정한 객체 데이터의 index번호를 찾을 때 유용
```js
const users = [
  { userId: '1', name: 'HEROPY' },
  { userId: '2', name: 'Neo' },
  { userId: '3', name: 'Amy' }
  { userId: '4', name: 'Evan' }
  { userId: '5', name: 'Lewis' }
]
const foundUserIndex = _.findIndex(users, { name: 'Amy' })
console.log(foundUserIndex)
// 2
```

### _.remove() 메소드
`_.remove(배열 데이터명, 찾을 데이터 조건)`  
내용이 많은 배열 데이터 안에서 특정한 객체 데이터를 삭제할 때 유용
```js
const users = [
  { userId: '1', name: 'HEROPY' },
  { userId: '2', name: 'Neo' },
  { userId: '3', name: 'Amy' }
  { userId: '4', name: 'Evan' }
  { userId: '5', name: 'Lewis' }
]
_.remove(users, { name: 'HEROPY' })
console.log(users)
/*[{ userId: '2', name: 'Neo' },
  { userId: '3', name: 'Amy' }
  { userId: '4', name: 'Evan' }
  { userId: '5', name: 'Lewis' }]*/
```
### _.cloneDeep() 메소드
내부의 모든 참조 관계까지 새로운 메모리로 복사
- 참조형 데이터(객체, 배열, 함수)를 복사할 때 그 안에 또 다른 참조형 데이터가 있다면 깊은 복사를 고려하여 사용

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

<dr/>

## JSON (JavaScript Object Notation)
.json이란 확장자를 가진 하나의 파일이 곧 하나의 데이터이다.  
(2가지 이상 데이터 입력 불가)
- undefined를 제외한 기본 데이터 타입을 동일하게 사용 가능하다.  
(단, 문자열(String)은 큰 따옴표(")로 구분)
- JSON은 사실 문자 데이터
- 최대한 경량화를 시켜야 하는 구조
- 단순하게 하나의 메모리만 참조할 수 있는 큰 덩어리의 문자 데이터로 관리가 됨

### 자바스크립트의 객체 표기법

```json
// myData.json

{
  "string": "HEROPY",
  "number": 123,
  "boolean": true,
  "null": null,
  "object": {},
  "array": []
}
```

```js
// main.js

import myData from './myData.json'  // 사실 .json은 문자 데이터

console.log(myData)
/* { string: "HEROPY",
     number: 123,
     boolean: true,
     null: null,
     object: {},
     array: [] } */

// 마치 객체 데이터처럼 보이지만 문자 데이터!
```

### `JSON.stringify()` 메소드
JavaScript파일 내부의 특정한 데이터를 JSON의 형태(포멧)로 문자 데이터화 시켜줌  
객테 데이터 뿐만 아니라 JavaScript에서 사용하는 모든 데이터를 인수로 사용 가능


### `JSON.parse()` 메소드
`stringify()`메소드와 반대로  
JSON 데이터를 JavaScript에서 활용할 수 있는 데이터로 재조립

```js
const user = {
  name: 'Heropy', 
  age: 85, 
  emails: [
    'thesecon@gmail.com',
    'neo@zillinks.com'
    ]
}
console.log(user)
/* {name: 'Heropy', age: 85, emails: Array(2)} */

const str = JSON.stringify(user)
console.log(str)
/* {"name":"Heropy", "age":85, "emails":["thesecon@gmail.com",
"neo@zillinks.com"]} */
console.log(typeof str) 
// string

const obj = JSON.parse(str)
console.log(obj)
/* {name: 'Heropy', age: 85, emails: Array(2)} */
```

<dr/>

## Storage
브라우저의 데이터를 저장하는 장소  
해당하는 도메인 주소(하나의 사이트)에 종속되어 저장

프로젝트 개발 서버로 브라우저를 열어  
개발자 관리 도구의 Application 탭 안에서  
Storage의 Local Storage 목록 중 데이터를 저장할 주소를 누르면  
key: value 형태 테이블이 보이는데 그 곳에 저장한 데이터가 입력됨.

### localStorage
데이터가 만료되지 않음 (따로 삭제하지 않는 이상 반영구적)  

#### `localStorage.setItem()` 메소드
key: value 형태로 데이터로 localStorage에 **저장** (문자 데이터로 저장하길 권장)
```js
localStorage.setItem('key', 'value') // 인수는 문자 데이터로 입력
```

#### `localStorage.getItem()` 메소드
localStorage에 저장한 데이터를 **읽기** 위해 사용
```js
localStorage.getItem('key') // key값만 인수로 입력
```

#### `localStorage.removeItem()` 메소드
localStorage에 저장한 데이터를 **삭제**하기 위해 사용
```js
localStorage.removeItem('key') // key값만 인수로 입력
```

#### 객체 데이터 localStorage에서 관리하기
```js
const user = {
  name: 'Heropy', 
  age: 85, 
  emails: [
    'thesecon@gmail.com',
    'neo@zillinks.com'
  ]
}

localStorage.setItem('user', JSON.stringify(user))
 // JSON.stringify 메소드를 이용해 객체데이터를 문자 데이터화 시켜 저장
 console.log(JSON.parse(localStorage.getItem('user')))
 // 문자 데이터화 시킨 데이터를 JS데이터로 전환
```
#### localStorage에 저장된 객체 데이터 수정하기
```js
const user = {
  name: 'Heropy', 
  age: 85,             // age: 22로 변경
  emails: [
    'thesecon@gmail.com',
    'neo@zillinks.com'
  ]
}

const str = localStorage.getItem('user')
const obj = JSON.parse(str)
// JS 데이터인 일반 객체 데이터로 전환
obj.age = 22
localStorage.setItem('user', JSON.stringify(obj))
// 문자 데이터화 시켜 저장
```


### sesseionStorage
페이지를 닫을 때 데이터가 사라짐

### Lowdb 패키지
웹 브라우저에서 사용할 수 있는 작은 JSON 데이터 기반의 데이터베이스  
lodash 패키지를 기반으로 동작하는 패키지

## API

### Query String
문자 데이터로 검색  
특정한 주소로 접근을 할 떄 기본적인 그 페이지에 대한 옵션을 명시하는 용도로 활용하는 문자
```js
주소?속성=값&속성=값&속성=값...

// 데이터 요청이 가능한 특정한 주소
```

### axios
Promise 기반의 브라우저 환경, node.js에서도 사용할 수 있는 HTTP 클라이언트 요청을 처리해 줄 수 있는 JavaScript 패키지  
- Promise: JavaScript에서 사용할 수 있는 특정한 객체
- Query String 주소로 받은 데이터를 JS로 활용할 수 있도록 도와주는 패키지

```js
import axios from 'axios'

function fetchMovies() {
  axios
    .get('https://www.omdbapi.com/?apikey=7035c60c&s=frozen')
    .then(res => {
      console.log(res)
      const h1El = document.querySelector('h1')
      const imgEl = document.querySelector('img')
      h1El.textContent = res.data.Search[0].Title
      imgEl.src = res.data.Search[0].Poster
    })
}
fetchMovies()
```