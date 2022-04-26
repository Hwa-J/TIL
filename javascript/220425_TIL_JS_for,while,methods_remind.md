## for

```js
// for (초기화; 조건; 평가식) {}
for (시작조건(초기화); 종료조건; 변화조건) {
}
```

```js
// for (시작; 종료; 변화) {}

const ulEl = document.querySelector('ul')

for (let i = 0; i < 10; i += 1) {
  const liEl = document.createElement('li')
  liEl.textContent = i
  ulEl.appendChild(liEl)
}
```

```js
// for of - 배열


const user = [
  { name: 'Heropy', age: 85 },
  { name: 'Neo', age: 22 },
  { name: 'Lewis', age: 8 },
]
for (const u of users) {
  console.log(u)
}

// for (시작; 종료; 변화) {}


for (let i =0; i < users.length; i+=1 ) {
  consol.log(users[i])
}
```
```js
// for in - 객체


const heropy = {
  name: 'Heropy',
  age: 85,
  isValid: true
}
for (const key in heropy) {
  console.log(heropy[key])
}
```

## while

```js
// while 
// 조건이 참(Truthy)이면 무한반복
// 조건이 거짓(falsy)이면, 0번 실행 


let i =0 // 시작
while (i < 3) { // 종료
  console.log(i)
  i += 1 // 변화
}
```
```js
// do while
// 조건이 거짓(falsy)이어도, 무조건 1번은 실행


let j =0 // 시작
do {
  console.log(i)
  j += 1 // 변화
} while (j < 3) { // 종료
```

<br/>

## 표준 내장 객체(메소드)



### 문자

#### `.length` 속성
문자의 개수(길이)를 숫자 데이터로 반환
```js
const str = 'Hello world'
str.length // 01234567890
console.log(str.length)  // 11
```

#### `.includes()` 메소드
인수로 들어간 문자가 포함되었는지 확인 (Boolean 반환)
```js
const str = 'The brown fox jumps over the lazy dog.'
console.log(str.includes('heropy'))  // false
```

#### `.indexOf()` 메소드
인수로 들어간 문자가 시작하는 위치(index 번호) 하나만 반환  
- 중복된 여러개 있어도 **맨 처음** 발견된 문자의 index값 반환
- 일치하는 문자가 없으면 -1 반환
```js
const str = 'The brown fox jumps over the lazy dog.'
console.log(str.indexOf('fox'))  // 10
console.log(str.indexOf('heropy'))  // -1
```

#### `.match()` 메소드
정규표현식의 조건과 일치하는 문자들을 배열 데이터로 반환
```js
const str = 'Hello world'
console.log(
// 문자.match(정규표현식)
  str.match(/^.*(?=\s)/gi) // ['Hello']
)
console.log(
  str.match(/^.*(?=\s)/gi)[0] // Hello
)
```

#### `.replace()` 메소드
문자를 대체할 때 사용 (삭제할 때도 사용 가능)
```js
const str = 'Hello world!'
console.log(
  str.replace('world', 'Heropy') // Hello Heropy!
)
```
- 삭제할 때
```js
const str = 'Hello world!'
console.log(
  str.replace('!', '') // Hello world
)
```
- 정규식 사용
```js
const str = 'Hello world!'
console.log(
  str.replace(/H../g, '') // lo world!
)
```

#### `.slice()` 메소드
두번째 인수(index)의 **직전** 문자까지 출력
```js
const str = 'Hello world!'
console.log(
  str.slice(0, 4) // Hell
)
```
```js
// -1은 가장 마지막 문자를 뜻함

const str = 'Hello world!'
console.log(
  str.slice(0, -1) // Hello world
)
```

#### `.split()` 메소드
인수로 들어간 문자기준으로 문자열을 쪼개서 배열로 반환
```js
const str = 'Hello world!'
console.log(
  str.split(' ') // ['Hello', 'world!']
)
```
```js
const str = 'apple, banana, cherry, orange'
console.log(
  str.split(', ')// 공백까지 인수로 넣어야 단어 단위로 쪼개짐
  // ['apple', 'banana', 'cherry', 'orange']
)
```

#### `.toUpperCase()` 메소드
대문자 변환
```js
const str = 'Hello world!'
console.log(
  str.toUpperCase() // HELLO WORLD!
)
```

#### `.toLowerCase()` 메소드
소문자 변환
```js
const str = 'HELLO WORLD!'
console.log(
  str.toLowerCase() // hello world!'
)
```
#### `.trim()` 메소드
공백문자 제거  
아이디, 패스워드 받을때 많이 쓰임
```js
const str = ' Hello world!      '
console.log(
  str.trim() // Hello world!
)
```

<br/>

### 숫자

#### `.toFixed()` 메소드
지정한 소수점 자리수까지 자르고 문자 데이터로 반환
```js
const num = 3.141592
console.log(
  num.tiFixed(2) // 3.14 (문자 데이터)
)
console.log(
  parseFloat(num.tiFixed(2)) // 3.14 (숫자 데이터)
)
```

#### `Number.isNaN()` 정적(Static) 메소드
데이터 타입이 숫자가 아닌지 판별
```js
isNaN() // 사용 X
Number.isNaN()  // 사용 권장

const num = 3.141592
console.log(
  Number.isNaN(num * undefined) // true
)
```

#### `Number.parseInt()` 정적(Static) 메소드
소수점 없애고 숫자 데이터로 반환
```js
const num = 3.141592
console.log(
  parseInt(num) // 3
)
```

#### `Number.parseFloat()` 정적(Static) 메소드
소수점을 유지한 채 숫자 데이터로 반환
```js
const num = '3.141592'
console.log(
  parseFloat(num) // 3.141592 (숫자 데이터)
)
```
- Number()객체
```js
const num = '3.141592'
console.log(
  Number(num) // 3.141592 (숫자 데이터)
)
```

<br/>

### Math

#### `Math.abs()` 정적(Static) 메소드
절대값으로 반환
```js
const num = -7
console.log(
  Math.abs(num) // 7
)
```

#### `Math.ceil()` 정적(Static) 메소드
올림값으로 반환
```js
const num = 0.45
console.log(
  Math.ceil(num) // 1
)
```
#### `Math.round()` 정적(Static) 메소드
반올림값으로 반환
```js
const num = 0.45
console.log(
  Math.round(num) // 0
)
```
#### `Math.floor()` 정적(Static) 메소드
내림값으로 반환
```js
const num = 0.45
console.log(
  Math.floor(num) // 0
)
```
#### `Math.min()` 정적(Static) 메소드
인수들 중 가장 작은 값을 반환
```js
console.log(
  Math.min(0, 1, 45, 757, 35, -2) // -2
)
```
#### `Math.max()` 정적(Static) 메소드
인수들 중 가장 큰 값을 반환
```js
console.log(
  Math.max(0, 1, 45, 757, 35, -2) // 757
)
```
#### `Math.random()` 정적(Static) 메소드
난수 반환 (랜덤한 수 반환)
```js
function getRandom(min, max) {
  return Math.floor(Math.random() * (max - min) + min
}
console.log(
  getRandom(0, 9) // 0~9사이 값을 랜덤하게 반환
)
```

<br/>

### 배열

 > (참고)  
 콜백함수를 사용하는 모든 메소드는 두번쨰 매개변수로 index값이 들어간다.  
 (세번째 매개변수는 배열 자체가 들어가지만 잘 사용하지 않음)

#### `.length` 속성
배열 데이터의 아이템 개수를 반환
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.length // 4
)
```

#### `.concat()` 메소드
주어진 배열이나 값들을 기존 배열에 합쳐 새 배열로 반환  
원본 수정 X  
`기존배열.concat(새로운배열1, 새로운배열2, 새로운배열3, ...)`
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.concat([4, 5, 6]) // [1, 2, 3, 4, 4, 5, 6]
)
console.log(arr) // [1, 2, 3, 4]
```
##### `.every()` 메소드  
배열에서 **모든** 요소(아이템)가 (콜백)함수조건을 만족하는지 판별 
(Boolean 반환)
- 배열을 아이템 개수만큼 실행
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.every(item => item < 5) // true
)
console.log(
  arr.every(item => item < 4) // false
)
```
##### `.filter()` 메소드  
(콜백)함수조건을 만족하는 **모든** 요소(아이템)를 모아 새로운 배열로 반환  
- 배열을 아이템 개수만큼 실행
- 원본 데이터보다 개수가 줄어든 배열 반환
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.filter(item => item < 3) // [1, 2]
)
```

##### `.find()` 메소드  
(콜백)함수조건을 만족하는 첫번째 요소(아이템)를 반환 
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.find(element => element < 3) // 1
)
```
```js
const user = [
  { name: 'Heropy', age: 85 },
  { name: 'Amy', age: 85 }
]
const foundUser = users.find(user => user.name === 'Heropy')
console.log(foundUser) // { name: 'Heropy', age: 85 }
```

##### `.findIndex()` 메소드  
(콜백)함수조건을 만족하는 첫번째 요소(아이템) index 번호 반환 
```js
const arr = [1, 2, 3, 4]
console.log(
  arr.findIndex(item => item === 3) // 2
)
```
- 응용 (배열 아이템 중 숫자 3 삭제)
```js
const arr = [1, 3, 2, 4]
arr.splice(
  arr.findIndex(item => item === 3), 
  1
  )
```

##### `.forEach()` 메소드  
```js
const arr = [1, 3, 2, 4]

// for 

for (let i = 0; i < arr.length; i += 1) {
  
  if (i === 3) {
    break // break 키워드로 실행 중간에 멈출 수 있음
  } 
 console.log(arr[i])
}


// for of

for (const item of arr) {
  console.log(item)
}


// forEach
// 모든 아이템을 순환할 떄까지 멈출 수 없음

arr.forEach(item => {
  console.log(item)
})
```
##### `.includes()` 메소드  
```js
const arr = [1, 3, 2, 4, 5]
console.log(
  arr.includes(4) // true
)
console.log(
  arr.includes(7) // false
)
```

##### `.join()` 메소드  
인수를 기준으로 배열의 모든 요소를 연결해 하나의 문자열로 만듦
```js
const arr = [1, 2, 3, 4]

console.log(arr.join(', '))
// 1, 2, 3, 4 (문자 데이터 반환)

console.log(arr.join('/'))
// 1/2/3/4 (문자 데이터 반환)
```
```js
const arr = ['AR', '패션', '스포츠', '인테리어']

console.log(arr.join('/'))
// AR/패션/스포츠/인테리어
```

#### `.map()` 메소드
모든 요소(아이템)에 각각 (콜백)함수에서 **반환된 결과(데이터)를 모아** 새로운 배열로 반환
```js
const arr = ['AR', '패션', '스포츠', '인테리어']

console.log(
  arr.map(item => {
    return {
      name: item
    }
  })
)
// [{name: 'AR'}, [{name: '패션'}, [{name: '스포츠'}, [{name: '인테리어'}]
```
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.map(item => {
    return item * 2
  })
)
// [2, 6, 4, 8]
```
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.map((item, index)=> {
    console.log(index) 
    // 두번째 인수로 index값을 받을 수 있다 (몇번째 아이템의 결과값인지 확인 가능)
    return item * 2
  })
)
// [2, 6, 4, 8]
```

#### `.pop()` 메소드
기존 배열의 맨뒤 아이템 삭제
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.pop()
) // 4
console.log(arr) // [1, 3, 2]
```

#### `.shift()` 메소드
기존 배열의 맨앞 아이템 삭제
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.shift()
) // 1
console.log(arr) // [3, 2, 4]
```


#### `.push()` 메소드
인수로 받은 값을 기존 배열의 맨 뒤에 여러 아이템을 추가
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.push(99, 7, 123)
) // 1
console.log(arr) // [1, 3, 2, 4, 99, 7, 123]
```


#### `.unshift()` 메소드
인수로 받은 값을 기존 배열의 맨 앞에 여러 아이템을 추가
```js
const arr = [1, 3, 2, 4]

console.log(
  arr.unshift(99, 7, 123)
) // 1
console.log(arr) // [99, 7, 123, 1, 3, 2, 4]
```