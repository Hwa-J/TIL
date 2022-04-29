# SCSS
CSS 전처리기  
: CSS를 조금 더 쉽게 사용하기 위한 도구

SaSS문법을 컴파일을 통해 표준 CSS로 변환

## SCSS 작성문 CSS 변환 미리보기 사이트
> https://www.sassmeister.com/  
SCSS 작성문이 어떻게 CSS로 변환되는지 바로 확인 할 수 있다.


## 주석

```scss
/* CSS와 동일 */
// SCSS에서 사용 가능
```
- `/**/`  
CSS로 컴파일(변환)시 주석처리된 상태 그대로 들어감    
- `//`  
CSS로 컴파일(변환)시 내용이 사라짐


## 중첩

CSS에서 상위 선택자를 하위요소를 지정할 떄마다 반복적으로 작성해야 했지만,  
SCSS에선 중첩 작성이 가능해 하나의 상위 선택자 내부에 하위요소들을 작성할 수 있다.

```scss
// SCSS

.container {
 > ul {
    li {
        font-size: 40px;
        .name {
          color: royalblue;
        }
        .age {
            color: orange;
        }
      }
    }
}
```
```css
/* CSS */

.container > ul li {
  font-size: 40px;
}
.container > ul li .name {
  color: royalblue;
}
.container > ul li .age {
  color: orange;
}
```

## 상위(부모) 선택자 참조
`&` 특수기호를 이용해 상위 선택자를 참조(치환)할 수 있다.
```scss
// SCSS

// & - 상위 선택자 참조

.btn {
  position: absolute;
  &.active {
    color: red;
  }
}

.list {
  li{
    &:last-child {
      margin-right: 0;
    }
  }
}

.fs {
  &-small { font-size: 12px; }
  &-medium { font-size: 14px; }
  &-large { font-size: 16px; }
}
```

```css
/* CSS */

.btn {
  position: absolute;
}
.btn.active {
  color: red;
}

.list li:last-child {
  margin-right: 0;
}

.fs-small {
  font-size: 12px;
}
.fs-medium {
  font-size: 14px;
}
.fs-large {
  font-size: 16px;
}
```

## 중첩된 속성

네임스페이스를 가진 속성도 중첩 사용이 가능하다.
### 네임스페이스  
**이름을 통해** 구분 가능한 범위를 만들어내는 것으로 일종의 **유효범위를 지정**하는 방법을 말합니다.
```scss
// SCSS

// 중첩된 속성

.box {
  font: {
    weight: bold;
    size: 10px;
    family: sans-serif;
  };
  margin: {
    top: 10px;
    left: 20px;
  };
  padding: {
    top: 10px;
    bottom: 40px;
    left: 20px;
    right: 30px;
  };
}

// font-, margin-, padding-들은 네임스페이스를 가진다.
```

```css
/* CSS */

.box {
  font-weight: bold;
  font-size: 10px;
  font-family: sans-serif;
  margin-top: 10px;
  margin-left: 20px;
  padding-top: 10px;
  padding-bottom: 40px;
  padding-left: 20px;
  padding-right: 30px;
}
```

## 변수
`$` 특수기호를 이용해 변수선언을 하고 재활용 할 수 있다.  
- 재활용 가능  
  (반복 사용, 주요하게 쓰이는 색상 등에 활용할 떄 유용함)
- {중괄호} 안에서 선언할 경우 유효범위가 {중괄호} 내부로 설정됨  
  (밖에서 선언하면 전역변수)
- 값 재할당 가능 (let과 동일)

```scss
// 변수 (Variables)

$size: 100px;  // 변수 선언

.container {
  position: fixed;
  top: $size;
  .item {
    width: $size;
    height: $size;
    transform: translateX($size);
  };
}
```

```css
/* CSS */

.container {
  position: fixed;
  top: 100px;
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px);
}
```
- 재할당
```scss


.container {
  $size: 200px;  // 변수 선언
  position: fixed;
  top: $size;
  .item {
    $size: 100px;  // 재할당
    width: $size;
    height: $size;
    transform: translateX($size);
  }
  left: $size;  // 마지막 재할당 값으로 들어감
}
```

```css
/* CSS */

.container {
  position: fixed;
  top: 200px;
  left: 100px;  /* 마지막 재할당 값으로 들어감 */
}
.container .item {
  width: 100px;
  height: 100px;
  transform: translateX(100px);
}
```

## 산술연산

```scss
div {
  width: 20px + 20px;
  height: 40px - 10px;
  font-size: 10px * 2;
  margin: 30px / 2;  // 연산 불가
  padding: 20px % 7;
}
```

```css
/* CSS */

div {
  width: 40px;
  height: 30px;
  font-size: 20px;
  margin: 30px/2;  /* 연산 불가 */
  padding: 6px;
}
```

- 나눗셈 `/` 특수기호로만 안되는 이유  
나눗셈 연산자가 아닌 단축 속성의 구분자로 인식해서 불가
 ```scss
span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  font: 10px / 10px serif;
}
```
```css
/* CSS */

span {
  font-size: 10px;
  line-height: 10px;
  font-family: serif;
  font: 10px/10px serif;
}
```
### 나눗셈 연산자 사용하기
```scss
div {
  $size: 30px;
  margin: (30px / 2);
  margin: ($size / 2);
  margin: 10px + 12px / 2;
}
```
```css
/* CSS */

div {
  margin: 15px;
  margin: 15px;
  margin: 16px;
}
```
### 다른 단위 값 연산하기 (calc)
```scss
div {
  width: calc(100% - 200px);
}
```
```css
/* CSS */

div {
  width: calc(100% - 200px);
}
```

## 재활용(Mixins)

### `@mixin` (저장)
@mixin 키워드를 통해 설정한 이름 안에 속성들을 묶어서 재활용 할 수 있다. (변수와 비슷)  
### `@include` (불러오기)
사용할 때엔 @include 키워드로 변수명을 작성해 속성을 불러올 수 있다.

```scss
@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  @include center;
  .item {
    @include center;
  }
}
.box {
  @include center;
}
```

```css
/* CSS */

div {
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
.container .item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## 매개변수 활용
@mixin 키워드를 통해 설정한 이름에 매개변수를 설정해 인수를 받을 수 있다. (함수와 비슷)

```scss
@mixin box($size) {  // 매개변수 설정
  width: $size;
  height: $size;
  background-color: tomato;
}
.container {
  @include box(200px);
  .item {
    @include box(100px);
  }
}
.box {
  @include box(100px);
}
```
```css
/* CSS */

.container {
  width: 200px;
  height: 200px;
  background-color: tomato;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: tomato;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```


### 매개변수 기본값
매개변수 옆에 : 콜론기호를 작성해 기본값을 설정할 수 있다.  
- 인수는 작성 순서대로 매개변수로 들어감!  
- 인수 순서와 상관없이 하나의 매개변수의 값만 넣고싶다면,   
  인수로 매개변수 명과 함꼐 값을 지정한다 (키워드 인수 문법) 

```scss
@mixin box($size: 100px, $color: tomato) {  // :기호로 기본값 설정
  width: $size;
  height: $size;
  background-color: $color;
}
.container {
  @include box(200px, red);
  .item {
    @include box($color: green);
  }
}
.box {
  @include box;
}
```
```css
/* CSS */

.container {
  width: 200px;
  height: 200px;
  background-color: red;
}
.container .item {
  width: 100px;
  height: 100px;
  background-color: green;
}

.box {
  width: 100px;
  height: 100px;
  background-color: tomato;
}
```

## 반복문
```scss
// 1부터 10까지 반복하겠다.
@for $i from 1 through 10 {반복할 내용} 
```

- JS와 다르게 1번부터 시작!  
- 값을 지정하는 자리가 아닌 곳엔 `#{데이터}` 보간법으로 데이터를 넣을 수 있다.
- 순서대로 넣어야 하는 이미지를 불러올 때 유용하다.
```scss
// for (let i = 0; i< 5; i +=1) {
//  console.log(`loop-${i}`)  
// }

@for $i from 1 through 5 {
  .box:nth-child(#{$i}) {
    width: 100px * $i;
  }
}
```
```css
/* CSS */

.box:nth-child(1) {
  width: 100px;
}

.box:nth-child(2) {
  width: 200px;
}

.box:nth-child(3) {
  width: 300px;
}

.box:nth-child(4) {
  width: 400px;
}

.box:nth-child(5) {
  width: 500px;
}
```

## 함수
```scss
// JS 함수와 작성법 유사  

@function 함수이름 (매개변수1, 매개변수2 ...) {
  @return $매개변수1 * $매개변수2
}
```



```scss
// @mixin은 속성들의 묶음
// @functio은 속성의 값을 계산할 때

@mixin center {
  display: flex;
  justify-content: center;
  align-items: center;
}
@function ratio ($size, $ratio) {
  @return $size * $ratio
}

.box {
  $width: 160px;
  width: $width;
  height: ratio($width, 9/16);  // 유튜브 화면비율
  @include center;
}
```

## 색상 내장 함수

### `mix()` 함수
인수의 색깔을 모두 섞은 색상을 반환한다.

### `lighten()`, `darken()` 함수

- lighten()  
첫번째 인수의 색상을 두번쨰 인수의 값만큼 밝아짐  
```scss
background-color: lighten(매개변수, 값)
```
- darken()  
첫번째 인수의 색상을 두번쨰 인수의 값만큼 어두워짐  
```scss
background-color: darken(매개변수, 값)
```
- 응용 (hover했을때 어두워짐)  
```scss
&:hover {
  background-color: darken($color, 10%)
}
```
### `saturate()`, `desaturate()` 함수
- saturate()  
첫번째 인수의 색상을 두번쨰 인수의 값만큼 채도가 높아짐
- desaturate()
첫번째 인수의 색상을 두번쨰 인수의 값만큼 채도가 낮아짐

### `grayscale()` 함수
인수의 색상을 회색으로 만들어줌 (인수 1개만 있으면 됨!)

### `invert()` 함수
인수의 색상을 반전된 색상으로 만들어줌

### `rgba()` 함수
첫번째 인수의 색상을 두번쨰 인수의 값만큼 투명해짐

<br/>

## 가져오기
`@import` 키워드를 통해 다른 scss파일을 연결시킬 수 있다.
- url 키워드 생략 가능
- 확장자 명 생략 가능
- , 쉼표 기호로 구분하여 여러 파일을 연결시킬 수 있음
```scss
@import "./sub", "./sub2"
```

## 데이터 종류

```scss
$number: 1;     // .5, 100px, 1em
$string: bold;  // relative, "../images/a.png"
$color: red;    // blue, #FFF00, rgba(0,0,0,.1)
$boolean: true; // false
$null: null;
// 배열 데이터와 유사
$list: orange, royalblue, yellow;  
// 객체 데이터와 유사
$map: (
  o: orange,
  r: royalblue,
  y: yellow
);

.box {
  width: 100px;
  color: red;
  position: null;  // css변환시 사라짐
}
```
```css
.box {
  width: 100px;
  color: red;
}
```

<br/>

## 반복문 @each
list, map 데이터를 활용한 반복문  
- list  
```scss
$list: orange, royalblue, yellow;  

@each $c in $list {
  .box {
    color: $c;
  }
}
```
```css
.box {
  color: orange;
}

.box {
  color: royalblue;
}

.box {
  color: yellow;
}
```
- map  
key: value형태의 데이터를 불러와 사용
```scss
$map: (
  o: orange,
  r: royalblue,
  y: yellow
); 

@each $key, $value in $map {
  .box-#{$key} {
    color: $value;
  }
}
```
```css
.box-o {
  color: orange;
}

.box-r {
  color: royalblue;
}

.box-y {
  color: yellow;
}
```
<br/>

## 재활용 @content
@mixin으로 지정한 기본적인 내용에 추가적인 내용을 더할 수 있도록 하는 키워드
```scss
@mixin left-top {
  position: absolute;
  top: 0;
  left: 0;
  @content;
}
.container {
  width: 100px;
  height: 100px;
  @include left-top;
}
.box {
  width: 200px;
  height: 300px;
  @include left-top {
    bottom: 0;
    right: 0;
    margin: auto;
  }
}
```
```css
.container {
  width: 100px;
  height: 100px;
  position: absolute;
  top: 0;
  left: 0;
}

.box {
  width: 200px;
  height: 300px;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  margin: auto;
}
```