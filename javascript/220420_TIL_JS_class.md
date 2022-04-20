## 조건문


### If Else

```js
if (a === 0) {
  console..log('a is 0')
} else if (a === 2) {
  console..log('a is 2')  
} else if (a === 4) {
  console..log('a is 4')
} else {
  console.log('rest...')
}
```

### Swich

 하나의 case 내용이 끝나면 꼭! break 키워드 붙이기  
 안 붙이면 다른 부분의 내용도 실행 될 수 있음  
 변수의 내용이 정확히 무엇인지 구분해서 조건문 작성 가능  
 특정한 데이터가 무엇으로 딱 떨어지는 조건문 작성 시 if문 보다 유용

```js
switch (a) {
  case 0:
    console.log('a is 0')
    break  // 하나의 case 내용이 끝나면 break 키워드 붙이기
  case 2:
    console.log('a is 2')
    break
  case 4:
    console.log('a is 4')
    break
  default:
    console.log('rest...')
}
```

### 반복문 (For statement)

```js
// for (시작조건; 종료조건; 변화조건) {}
for (let i = 0; i <3; i += 1) {
  console.log(i)   // 0 1 2 각각 출력됨
}
```
```js
const ulEl = document.querySelector('ul')

for (let i = 0; i <3; i += 1) {
  const li = document.createElement('li')
  li.textContent = `list-${i + 1}`
  ulEl.appendChild(li)
}
// HTML 구조에 실제 존재하지 않지만
// JS로 요소를 생성해서 실제 HTML 구조인 ul태그의 자식으로
// 빈복문을 통해 내용을 삽입
```
```js
const ulEl = document.querySelector('ul')

for (let i = 0; i <10; i += 1) {
  const li = document.createElement('li')
  li.textContent = `list-${i + 1}`
  if ((i + 1) % 2 === 0) {
    li.addEventListener('click', function () {
      console.log(li.textContent)
    })
  }
  ulEl.appendChild(li)
}
// 짝수를 눌렀을 때 console창에 클릭한 요소의 내용이 나옴
```

## 변수의 유효범위 (Varial Scope)
해당하는 변수가 유효하게 동작할 수 있는 특정 범위  
- const, let (블록 레벨)
- var (함수 레벨)

```js
// let, const
function scope() {
  if (true) {
    const a = 123
    console.log(a)
  }
}
scope()

// var
function scope() {
  if (true) {
    const a = 123
  }
  console.log(a)
}
scope()
```

## 형 변환(Type conversion)
자료형의 데이터 타입

```js
const a = 1
const b = '1'

console.log(a == b) // true
```
`== 동등 연산자`를 많이 쓰지 않음  
의도하지 않게 서로 다른 값이 같다라는 결과를 가질 수 있어서  
`===일치 연산자`를 사용함





# 함수

함수를 호출하는 횟수를 최소화 하는 것이 좋음
함수의 결과가 반복적으로 사용될 떄는 변수에 담아서 사용
단일로 사용 될 때, 함수가 사용되는 곳에 직접 호출


## 화살표 함수

```js
// function () {}

const double = function (x) {
  return x * 2
}
console.log('double: ', double(7))


// () => {}

const doubleArrow = (x) => {
  return x * 2
}
console.log('doubleArrow', doubleArrow(7))

// () => {} 축약
const doubleArrow = x =>  x * 2
console.log('doubleArrow', doubleArrow(7))

// () => ({}) 객체 데이터 축약
const doubleArrow = x =>  ({ name: 'Heroppy '})
console.log('doubleArrow', doubleArrow(7))
```


## 타이머 함수

setTimeout(함수, 시간ms): 일정 시간 후 함수 실행
setInterval(함수, 시간ms): 시간 간격마다 함수 실행
clearTimeout(): 설정된 Timeout 함수를 종료
clearInterval(): 설정된 Interval 함수를 종료

```js
setTimeout(() => {
  console.log('Heropy!')
}, 3000)              // 3초 후에 콘솔 창에 Heropy! 출력
```
```js
const timer = setTimeout(() => {
  console.log('Heropy!')
}, 3000)              // 3초 후에 콘솔 창에 Heropy! 출력

const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
  clearTimeout(timer)
})   // h1태그를 클릭하면 timer기능을 사라지게 함
```
```js
const timer = setInterval(() => {
  console.log('Heropy!')
}, 3000)              // 3초마다 콘솔 창에 Heropy! 출력

const h1El = document.querySelector('h1')
h1El.addEventListener('click', () => {
  clearInterval(timer)
})   // h1태그를 클릭하면 timer기능을 사라지게 함
```

## 콜백 (Callback)
함수의 인수로 사용되는 함수 
실행 위치를 보장하는 용도

```js
function timeout(cb) {
  setTimeout(() => {
    console.log('Heropy!')
    cb()
  }, 3000)
}
timeout(() => {
  console.log('Done!')
})
```

# JS 클래스

하나의 객체 데이터가 가진  
모든 속성, 메소드를 묶어서 멤버(Member)라고 부름

```js
const heropy = {
  // 속성
  firstName: 'Heropy',
  lastName: 'Park',
  // 메소드 (함수를 가진 속성)
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`
    // 여기서 this는 heropy 변수를 지칭함
  }
}
console.log(heropy.getFullName()) // Heropy Park

const amy = {
  // 속성
  firstName: 'Amy',
  lastName: 'Clarke',
  // 메소드 (함수를 가진 속성)
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`
    // 여기서 this는 heropy 변수를 지칭함
  }
}
console.log(amy.getFullName()) // Amy Clarke

const neo = {
  // 속성
  firstName: 'Neo',
  lastName: 'Smith',
  // 메소드 (함수를 가진 속성)
  getFullName: function () {
    return `${this.firstName} ${this.lastName}`
    // 여기서 this는 heropy 변수를 지칭함
  }
}
console.log(neo.getFullName()) // Neo Smith
```


```js
// JS 클래스로 수정

function User(first, last) {
  this.firstName = first
  this.lastName = last
}
// 여기서 this는 아래 생성자 함수가 할당된 객체(heropy, amy, neo)를 지칭함

User.prototype.getFullName = function () {
  return `${this.firstName} ${this.lastName}`
}
// user라는 함수에 숨겨진 prototype이라는 속성에 getFullName메소드 할당
// 데이터 안에 멤버 외 속성 중 __proto__라는 객체 데이터 안에 할당된 것을 볼 수 있다.

const heropy = new User('Heropy', 'Park')
const amy = new User('Amy', 'Clarke')
const neo = new User('Neo', 'Smith')
// 여기서 user를 생성자 함수라 부른다 (하나의 객체 데이터가 생성됨)
// new라는 키워드로 생성자 함수로 실행한 결과를 반환해 할당된 변수를
// 생성자 함수의 인스턴스(heropy, amy, neo)라 부름

console.log(heropy.getFullName()) // Heropy Park
console.log(amy.getFullName())  // Amy Clarke
console.log(neo.getFullName())  // Neo Smith
```
`생성자 함수`    
하나의 데이터를 생성하는 함수  
일반 함수와 구분을 위해 Pascalcase(첫문자 부터 대문자)로 작성(개발자간 약속)  
함수를 사용해 new라는 키워드를 붙여 생성자 함수를 실행
`리터럴 방식`  
  특정 문자 기호만으로 데이터를 생성하는 방식  
`인스턴스`  
  new라는 키워드로 생성자 함수로 실행한 결과를 반환해 할당된 변수를  
  생성자 함수의 인스턴스라 부름  
`prototype` (중요!)  
로직에 변화가 없는 통일화 된 메모리를 효율적으로 관리  
몇 개의 데이터가 있던 메모리에 한번만 만들어짐

