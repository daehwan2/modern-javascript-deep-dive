# 생성자 함수
- **생성자함수**란 `new` 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다.
- 일반함수와 동일한 방법으로 생성자 함수를 정의하고 new 연산자와 함께 호출하면 해당함수는 생성자 함수로 동작한다.

### 객체 리터럴에 의한 객체 생성 방식의 문제점
```javascript
//동일한 프로퍼티를 갖는 객체를 여러 개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다

const circle1 = {
  radius: 5,
  getDiameter(){
    return 2 * this.radius;
  }
}

console.log(circle1.getDiameter()); // 10


const circle2 = {
  radius: 10,
  getDiameter(){
    return 2 * this.radius;
  }
}

console.log(circle2.getDiameter()); // 20
```

### 생성자 함수에 의한 객체 생성 방식의 장점
```javascript
// 생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기 위한 템플릿(클래스)처럼 
// 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getDiameter()); // 10
console.log(circle2.getDiameter()); // 20
```

### 생성자 함수의 인스턴스 생성 과정

1. 인스턴스 생성과 this 바인딩 ( 함수가 실행되는 런타임 이전에 발생 )
  1. 암묵적으로 빈객체 생성 => 인스턴스
  2. 인스턴스가 this에 바인딩
2. 인스턴스 초기화: 코드가 한줄씩 실행되어(개발자가 짠 코드) this에 바인딩되어 있는 인스턴스에 프로퍼티나 메서드를 추가하고 초기값을 할당한다.
3. 인스턴스 반환: 모든 처리가 끝나면 인스턴스가 바인딩된 this가 암묵적으로 반환된다. (다른객체를 명시적으로 반환하면 그 값이 반환되고, 만약 원시값을 반환했다면 무시되어서 this가 반환된다.)
> 따라서 생성자 함수 내부에서 return 문을 반드시 생략해야 한다.

### this

- **this**는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. 
- **this**가 가리키는 값, 즉 this 바인딩은 **함수 호출 방식**에 따라 동적으로 결정된다.

| 함수 호출 방식 | this가 가리키는 값(this 바인딩) |
| --- | --- |
| 일반 함수로서 호출 | 전역 객체 |
| 메서드로서 호출 | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수로서 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

```javascript
function foo(){
  console.log(this);
}

foo(); // window => node.js에서는 global

const obj = { foo };
obj.foo(); // obj

const inst = new foo(); //inst
```

### 바인딩

- 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 예를 들어, 변수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩하는 것이다.
- this 바인딩은 this(키워드로 분류되지만 식별자 역할을 한다)와 this가 가리킬 객체를 바인딩하는 것이다.


### 내부 메서드 [[Call]] 과 [[Construct]]

- 함수객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드는 물론, 함수로서 동작하기 위해 함수 객체만을 위한 [[Environment]], [[FormalParameters]] 등의 내부 슬롯과 [[Call]], [[Construct]] 같은 내부메서드를 추가로 가지고 있다.
- 일반 함수로 호출되면 내부메서드 [[Call]]이 호출
- new연산자와 함께 생성자 함수로서 호출되면 내부 메서드 [[Construct]]가 호출
- [[Call]] 을 갖는 함수 객체를 **callable**
- [[Construct]]를 갖는 함수 객체를 **constructor**
- [[Construct]]를 갖지않는 함수 객체를 **none-constructor**

![image](https://user-images.githubusercontent.com/53414542/172410585-e171803a-8080-4743-9598-1669c19fe4da.png)

- constructor: 함수 선언문, 함수 표현식, 클래스(클래스도 함수다)
- none-constructor: 메서드(ES6 메서드 축약 표현), 화살표 함수


### 생성자 함수로 쓸려고 만들었는데 new로 호출하지 않았을 경우

#### new.target

```javascript
function Circle(radius){
  if(!new.target){ // 이 함수가 new 연사자와 함께 호출되지 않았다면 new.target은 undefined, 했으면 함수 자신
    return new Circle(radius);
  }
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

const circle = Circle(5);
console.log(circle.getDiameter()); // 10
```

#### 스코프 세이프 생성자 패턴

```javascript
function Circle(radius){
  if(!(this instanceof Circle)){ // 이 함수가 new 연사자와 함께 호출되지 않았다면 new.target은 undefined, 했으면 함수 자신
    return new Circle(radius);
  }
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

const circle = Circle(5);
console.log(circle.getDiameter()); // 10
```
