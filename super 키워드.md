# super

super 키워드는 함수처럼 호출할 수도 있고 this와 같이 식별자처럼 참조할 수 있는 특수한 키워드다.

- super를 호출하면 수퍼클래스의 constructor(super-constructor)를 호출한다
- super를 참조하면 수퍼클래스의 메서드를 호출할 수 있다.

```javascript
class Base{
  constructor(a, b) {
    this.a = a;
    this.b = b;
  }
}


class Derived extends Base {
  //암묵적으로 정의
  //constructor(...args) { super(...args); }
}

const derived = new Derived(1, 2);
console.log(derived); // Derived { a:1, b:2 }
```


### super 호출

1. 서브클래스에서 constructor를 생략하지 않는 경우 서브클래스의 constructor에서는 반드시 super를 호출해야한다.
2. 서브클래스의 constructor에서 super를 호출하기 전에는 this를 참조할 수 없다.
3. super는 반드시 서브클래스의 constructor에서만 호출한다. 서브클래스가 아닌 클래스의 constructor나 함수에서 super를 호출하면 에러가 난다.

<br/><br/><br/><br/>

### super 참조

1. 서브클래스의 프로토타입 메서드 내에서 super.sayHi는 수퍼클래스의 프로토타입 메서드 sayHi를 가리킨다.
2. 서브클래스의 정적 메서드 내에서 super.sayHi는 수퍼클래스의 정적 메서드 sayHi를 가리킨다.
