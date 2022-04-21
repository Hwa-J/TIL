# JS 데이터

## 문자 

`String` 전역 객체는 문자열(문자의 나열)의 생성자입니다.

```js
new String() //생성자 함수 방식

"", '', `` // 리터럴 방식(특정한 기호를 이용해 생성한 데이터)
```
<br/>

### String.prototype.Methods

<br/>

#### `.indexOf()` 메소드

`indexOf()` 메서드는 호출한 `String`객체에서 **주어진 값** 과 **일치** 하는  
**첫번째 인덱스를 반환**합니다.  
일치하는 값이 없으면 -1을 반환합니다.

```js
// String.prototype.indexOf()
// 'Hello world!'.indexOf 리터럴 방식 데이터에 직접 사용 가능

const result = 'Hello world!'.indexOf('Heropy')
console.log(result)    // -1 출력
```

<br/>

#### `.slice()` 메소드

`slice()` 메소드는 문자열의 **일부를 추출**하면서 **새로운 문자열을 반환**합니다.
0부터 시작하는 추출 종료점 인덱스로 그 직전까지 추출

```js
const str = 'Hello world!'

console.log(str.slice(6, 11))  // world 출력
```

#### `.length()` 메소드
문자의 개수를 세어줌

```js
const str = '0123'

console.log(str.length)  // 4 출력
console.log('01 23'.length)  // 5 출력
```

#### `.replace()` 메소드


```js
const str = 'Hello world!'

console.log(str.replace('wold', 'HEROPY'))  // Hello HEROPY 출력
console.log(str.replace(' wold', ''))  // Hello 출력
```

#### `.match()` 메소드

```js
const str = 'thesecon@Gmail.com'

console.log(str.match(/.+(?=@)/)[0])  // thesecon 출력
// 정규표현식(RegExp) /.+(?=@)/   
// @기호 앞에 있는 내용을 전부 추출
```

#### `.trim()` 메소드

```js
const str = '    Hello world   '

console.log(str.trim())  // Hello world 출력
// 앞뒤 공백문자 제거
```



## 숫자와 수학

<br/>

### Number.prototype.Methods

<br/>

#### `.toFixed()` 메소드


#### `.parseInt()` 메소드
전역(global) 함수로 어느 곳에서나 사용 가능

#### `.parseFloat()` 메소드
전역(global) 함수로 어느 곳에서나 사용 가능


```js
const pi = 3.14159265358979
console.log(pi)               // 3.14159265358979

const str = pi.toFixed(2)     // 소수점 2째 자리까지 표기(문자data 반환) 

console.log(str)              // 3.14
console.log(tyhpeof str)      // string

const integer = parseInt(str) // 정수로 변환
const float = parseFloat(str) // 소수로 변환

console.log(integer)          // 3
console.log(float)            // 3.14
console.log(tyhpeof integer, tyhpeof float)  // number number
```

<br/>

### Math.Methods

#### `Math.abs()` 메소드
주어진 숫자를 절대값으로 반환
```js
console.log( Math.abs(-12))     // 12
```
#### `Math.min()` 메소드
주어진 숫자 중 가장 작은값을 반환
```js
console.log( Math.min(2, 8))     // 2
```
#### `Math.max()` 메소드
주어진 숫자 중 가장 큰값을 반환
```js
console.log( Math.max(2, 8))     // 8
```
#### `Math.ceil()` 메소드
주어진 숫자를 소수점 아래 수를 올림한 값으로 반환
```js
console.log( Math.ceil(3.14))     // 4
```
#### `Math.floor()` 메소드
주어진 숫자를 소수점 아래 수를 내림한 값으로 반환
```js
console.log( Math.floor(3.14))     // 3
```
#### `Math.round()` 메소드
주어진 숫자를 소수점 아래 수를 반올림한 값으로 반환
```js
console.log( Math.round(3.14))     // 3
```
#### `Math.random()` 메소드
랜덤한 숫자(난수)값을 반환
```js
console.log( Math.random())     // 랜덤한 난수 출력
```
- 0 ~ 9까지 랜덤 숫자를 반환하는 함수
```js
function random() {
  return Math.floor(Math.random() * 10)
}
```

<br/>

## 배열

- 인덱스(Index)  
배열 데이터 내부에 들어있는 특정한 데이터의 위치를 가리키는 숫자
- 인덱싱(Indexing)  
대괄호 사이에 인덱스 숫자를 넣어 배열 데이터를 조회하는 방법
- 요소(element), 아이템(item)  
배열 데이터 내부에 있는 각각의 데이터를 지칭

<br/>

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(numbers[1])
console.log(fruits[2])
```

<br/>

### Array.prototype.Methods




#### `.length()` 메소드

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(numbers.length)  // 4
console.log(fruits.length)   // 3
console.log([1, 2]].length)  // 2
console.log([]].length)      // 0
```

#### `.concat()` 메소드
- 2개의 배열을 병합해 하나의 새로운 배열 데이터를 그 자라에 반환  
- 원본 데이터엔 영향이 없다


```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

console.log(numbers.concat(fruits))  // [1, 2, 3, 4, 'Apple', 'Banana', 'Cherry']
console.log(numbers)  // [1, 2, 3, 4]
console.log(fruits)   // ['Apple', 'Banana', 'Cherry']
```

#### `.forEach()` 메소드
배열 데이터의 아이템 개수만큼 특정한 콜백함수를 반복적으로 실행한는 용도 (반환X)
- 배열 데이터에서 forEach 메소드는 기본적으로 인수로 콜백함수를 받는다.  
- 콜백함수에 사용되는 매개변수들은 각각   
(배열의 아이템, 반복된 횟수, 원본의 배열데이터) 순서대로 매개변수로 제공한다.
- 원본 데이터엔 영향이 없다   

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

fruits.forEach(function (element, index, array) {
  console,log(element, index, array)
})
// Apple 0 ['Apple', 'Banana', 'Cherry']
// Banana 1 ['Apple', 'Banana', 'Cherry']
// Cherry 3 ['Apple', 'Banana', 'Cherry']


// 축약

fruits.forEach(function (fruit, i) {
  console,log(fruit, i)
})
// Apple 0
// Banana 1 
// Cherry 3 
```


#### `.map()` 메소드
인수로 사용되는 콜백함수가 반환한 데이터를 새로운 배열 데이터로 만들어 반환O
- 원본 데이터엔 영향이 없다

```js
// .forEach() vs .map()

const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

const a = fruits.forEach(function (fruit, index) {
  console.log(`${fruit}-${index}`)    // Apple-0
})                                    // Banana-1
                                      // Cherry-2
console.log(a)  // undefined

const b = fruits.map(function (fruit, index) {
  return(`${fruit}-${index}`)
})
console.log(b)  // ["Apple-0", "Banana-1", "Cherry-2"]
```

```js
// .map()

const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

const b = fruits.map(function (fruit, index) {
  return {
    id: index,
    name: fruit
  }
})
console.log(b)  
// [{id: 0, name: "Apple"}, {id: 1, name: "Banana"}, {id: 2, name: "Cherry"}]
```

```js
// 화살표 함수로 변경


const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

const a = fruits.forEach((fruit, index) => {
  console.log(`${fruit}-${index}`)    // Apple-0
})                                    // Banana-1
                                      // Cherry-2
console.log(a)  // undefined

const b = fruits.map((fruit, index) => ( {
    id: index,
    name: fruit
  }))
// [{id: 0, name: "Apple"}, {id: 1, name: "Banana"}, {id: 2, name: "Cherry"}]
```
>화살표 함수
>- 무명함수의 매개변수가 하나일 경우 (소괄호) 생략가능  
  `() => {}` → `  => {}`
>- 함수의 로직이 한 줄일 경우 return과 {중괄호} 생략가능  
`() => {return logic}` → `() => logic`
>- 로직이 하나일 경우 return과 {중괄호} 생략가능  
하지만, 함수의 반환값이 객체 데이터일 경우 객체데이터를 (소괄호)로 한번 감싸줘야 함  
`() => {return {logic}}` → `() => ({logic})`

<br/>

#### `.filter()` 메소드
인수로 사용되는 콜백함수가 반환한 데이터 중  
**true에 해당하는 데이터**만 모아 새로운 배열 데이터로 만들어 반환O
- 원본 데이터엔 영향이 없다

```js
const numbers = [1, 2, 3, 4]

const a = numbers.map(number => {
  return number < 3
})
console.log(a)  // [true, true, flase, false]

const b = numbers.filter(number => {
  return number < 3
})
console.log(b)  // [1, 2]

console.log(numbers)  // [1, 2, 3, 4]
```

```js
// 화살표 함수로 변환


const numbers = [1, 2, 3, 4]

const a = numbers.map(number => number < 3)
console.log(a)  // [true, true, flase, false]

const b = numbers.filter(number => number < 3)
console.log(b)  // [1, 2]

console.log(numbers)  // [1, 2, 3, 4]
```

<br/>

#### `.find()`, `.findIndex()` 메소드
`.find()`  
배열 데이터의 아이템 개수만큼 콜백함수를 반복적으로 실행하다가  
**true에 해당하는 데이터**를 찾으면 그 데이터만 반환하고 **멈춤**  
`.findIndex()`  
`.find()`메소드와 같이 실행하지만 반환 데이터의 index 값으로 반환

```js
const fruits = ['Apple', 'Banana', 'Cherry']


const a = fruits.find(fruit => {
  return /^B/.test(fruit)
  // ^B 맨 앞이 B로 시작하는 데이터
})
console.log(a)  // Banana를 출력하고 함수 멈춤(Cherry 안 봄)

const b = fruits.find(fruit => {
  return /^C/.test(fruit)
  // ^C 맨 앞이 C로 시작하는 데이터
})
console.log(b)  // Cherry

const c = fruits.findIndex(fruit => {
  return /^C/.test(fruit)
})
console.log(c)  // 2
```
```js
// 화살표 함수 변환

const fruits = ['Apple', 'Banana', 'Cherry']


const a = fruits.find(fruit => /^B/.test(fruit))
console.log(a)  // Banana

const b = fruits.find(fruit => /^C/.test(fruit))
console.log(b)  // Cherry

const c = fruits.findIndex(fruit => /^C/.test(fruit))
console.log(c)  // 2
```

<br/>

#### `.includes()` 메소드
배열 데이터에 인수로 들어온 데이터가 포함되어 있는지 확인 (불린데이터 반환)

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

const a = numbers.includes(3)
console.log(a)  // true

const b = fruits.includes('HEROPY')
console.log(b)  //false
```

<br/>

#### `.push()`, `.unshift()` 메소드 
- 원본 수정됨 주의!!  
`.push()`  
인수로 받은 값을 원본 배열 데이터 **맨 뒤**에 새로운 아이템으로 추가함
`.unshift()`  
인수로 받은 값을 원본 배열 데이터 **맨 앞**에 새로운 아이템으로 추가함

```js
const numbers = [1, 2, 3, 4]

numbers.push(5)
console.log(numbers)  // [1, 2, 3, 4, 5]

numbers.unshift(0)
console.log(numbers)  // [0, 1, 2, 3, 4, 5]
```

<br/>

#### `.reverse()` 메소드 
- 원본 수정됨 주의!!  
원본 데이터의 배열 순서를 거꾸로 뒤집는다. (index 변함)

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

numbers.reverse()
fruits.reverse()

console.log(numbers)  // [4, 3, 2, 1]
console.log(fruits)  // ['Cherry', 'Banana', 'Apple']
```
<br/>

#### `.splice()` 메소드 
- 원본 수정됨 주의!!  
원본 배열 데이터에서 **특정한 위치**의 아이템을 **삭제**하거나  
새로운 아이템을 **끼워 넣을 떄** 사용

`.splice(index, 삭제할 아이템 개수, 추가할 아이템 값)`

```js
const numbers = [1, 2, 3, 4]
const fruits = ['Apple', 'Banana', 'Cherry']

numbers.splice(2, 1, 99) // index 2위치에서 1개 아이템 삭제, 그 자리에 99 추가
console.log(numbers) // [1, 2, 99, 4]

fruits.splice(2, 0, 'Orange') // index 2위치에서 0개 아이템 삭제, 그 자리에 'Orange' 추가
console.log(fruits) // ['Apple', 'Banana', 'Orange', 'Cherry']

// 추가하지 않고 삭제도 가능
numbers.splice(2, 2) // index 2위치에서 2개 아이템 삭제
console.log(numbers) // [1, 2]
```