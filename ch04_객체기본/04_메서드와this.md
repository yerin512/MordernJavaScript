# 메서드와 this

객체는 사용자(user), 주문(order)등과 같이 실제 존재하는 개체(entity)를 표현하고자 할 때 생성된다.

```
let user = {
  name: "John",
  age: 30
};
```

사용자는 현실에서 장바구니에서 물건 선택하기, 로그인하기, 로그아웃 하기 등의 행동을 한다.
이와 마찬가지로 사용자를 나타내는 객체 user도 특정한 행동을 할 수 있다.

자바스크립트에선 객체의 프로퍼티에 함수를 할당해 객체에게 행동할 수 있는 능력을 부여해준다.

## 메서드 만들기

객체 user에게 인사할 수 있는 능력을 부여해주자.

```
let user = {
  name: "John",
  age: 30
};

user.sayHi = function() {
    alert('안녕하세요!');
    
};

user.sayHi(); //안녕하세요
```

함수 표현식으로 함수를 만들고, 객체 프로퍼티 user.sayHi에 함수를 할당해 주었다.
이제 객체에 할당된 함수를 호출하면 user가 인사를 해준다.
이렇게 객체 프로퍼티에 할당된 함수를 메서드(method)라고 부른다.


메서드는 이미 정의된 함수를 이용해서 만들 수도 있다.

```
let user = {
  // ...
};

// 함수 선언
function sayHi() {
  alert("안녕하세요!");
};

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi(); // 안녕하세요!
```


```
객체 지향 프로그래밍

객체를 사용해 개체를 표현하는 방식을 객체 지향 프로그래밍 (object-oriented programming, OOP) 라고 부른다.

OOP는 그 자체만으로도 학문의 분야를 만드는 중요한 주제다. 올바른 개체를 선택하는 방법, 개체 사이의 상호작용을 나타내는 방법 등에 관한 의사결정은 객체 지향 설계를 기반으로 이뤄진다.
객체 지향 프로그래밍 관련 추천도서로는 에릭 감마의  ‘GoF의 디자인 패턴’, 그래디 부치의 ‘UML을 활용한 객체지향 분석 설계’ 등이 있다.

```

## 메서드 단축 구문

객체 리터럴 안에 메서드를 선언할 때 사용할 수 있는 단축 문법이 있다.

```js
user = {
  sayHi: function() {
    alert("Hello");
  }

user = {
  sayHi() {
    alert("Hello");
  }
};
```

위 처럼 function을 생략해도 메서드를 정의할 수 있다.

## 메서드와 this

메서드는 객체에 저장된 정보에 접근할 수 있어야 제 역할을 할 수 있다. 모든 메서드가 그런 건 아니지만 대부분의 메서드가 객체 프로퍼티의 값을 활용한다.

user.sayHi()의 내부 코드에서 객체 user에 저장된 이름(name)을 이용해 인사말을 만드는 경우가 이런 경우에 속한다.

메서드 내부에서 this 키워드를 사용하면 객체에 접근할 수 있다.

이때 점 앞의 this는 객체를 나타낸다. 정확ㅎ는 메서드를 호출 할 때 사용된 객체를 나타냄.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다.
    alert(this.name);
  }

};

user.sayHi(); // John
```

user.sayHi()가 실행되는 동안에 this는 user를 나타낸다.
this를 사용하지 않고 외부 변수를 참조해 객체에 접근하는 것도 가능하다.

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert(user.name); // 'this' 대신 'user'를 이용함
  }

};
```

이렇게 외부 변수를 사용해 객체를 참조하면 예상치 못한 에러가 발생할 수 있다.
 user를 복사해 다른 변수에 할당하고, user는 전혀 다른 값으로 덮어썼다고 가정할 경우, sayHi()는 원치 않는 값을 참조한다.


```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
    alert( user.name ); // Error: Cannot read property 'name' of null
  }

};


let admin = user;
user = null; // user를 null로 덮어씁니다.

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참고하면서 에러가 발생했습니다.
```



alert 함수가 user.name 대신 this.name을 인수로 받았다면 에러가 발생하지 않는다.

## 자유로운 this

자바스크립트의 this는 다른 프로그래밍 언어의 this와 동작 방식이 다르다. 자바스크립트에선 모든 함수에 this를 사용할 수 있다.

```
function sayHi() {
  alert( this.name );
}
```
이래도 문법 에러가 발생하지 않는다. this의 값은 런타임에 결정된다. 컨텍스트에 따라 달라지는 것이다.

동일한 함수라도 다른 객체에서 호출했다면 this가 참조하는 값이 달라진다.



```js
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

// 별개의 객체에서 동일한 함수를 사용함
user.f = sayHi;
admin.f = sayHi;

// 'this'는 '점(.) 앞의' 객체를 참조하기 때문에
// this 값이 달라짐
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (점과 대괄호는 동일하게 동작함)
```


규칙은 간단하다. obj.f()를 호출했다면 this는 f를 호출하는 동안의 obj이다. 위 예시에선 obj가 user나 admin을 참조할 것이다.

#### 객체없이 호출하기 : this == undefined
객체가 없어도 함수를 호출할 수 있다.


```js
function sayHi() {
  alert(this);
}

sayHi(); // undefined
```

위와 같이 코드를 엄격 모드에서 실행하면 this엔 undefined가 할당된다. this.name으로 name에 접근하려고 하면 에러가 발생한다.

엄격모드가 아닐 땐 this가 전역 객체를 참조한다.
브라우저 환경에선 whidow라는 전역 객체를 참조한다.
 이런 동작 차이는 `user strict`가 도입된 배경이기도하다. 

 이런 식의 코드는 대개 실수로 작성되는 경우가 많다. 함수 본문에 this가 사용되었다면 객체 컨텍스트 내에서 함수를 호출할 것이라고 예상하면 된다.


#### 자유로운 this가 만드는 결과

다른 언어를 사용하다 자스로 넘어온 개발자는 this를 혼동하기 쉽다. this는 항상 메서드가 정의도니 객체를 참조할 것이라 착각한다.
이런 개념을 `bound this` 라고 한다.

자바스크립트에서 this는 런타임에 결정된다. 
메서드가 어디에서 정의되었는지에 상관없이 this는  점 앞의 객체가 무엇인가에 따라 자유롭게 결정된다.

this가 런타임에 결정되면 좋은 점도 있고 나쁜 점도 있다.
함수(메서드)를 하나만 만들어 여러 객체에서 재사용할 수 있다는 것은 장점이지만 이런 유연함이 실수로 이어질 수 있다는 것은 단점이다.



## this가 없는 화살표 함수

화살표 함수는 일반 함수와는 달리 `고유한` this를 가지지 않는다.
화살표 함수에서 this를 참조하면, 화살표 함수가 아닌 `평범한` 외부함수에서 this값을 가지고 온다.

아래 예시에서 함수 arrow()의 this는 외부 함수 user.sayHi()의 this가 된다.

```js
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // 보라
```

별개의 this가 만들어지는 건 원하지 않고, 외부 컨텍스트에 있는 this를 이요하고 싶은 경우 화살표 함수가 유용하다. 

```
화살표 함수를 사용하면 현재 컨텍스트를 잃지 않아 편리
this를 가지지 않습니다.
arguments를 지원하지 않습니다.
new와 함께 호출할 수 없습니다.
```

## 요약

- 객체 프로퍼티에 저장된 함수를 메서드라고 부른다.
- object.doSometing() 은 객체를 행동할 수 있게 해준다.
- 메서드는 this로 객체를 참조한다.

this 값은 런타임에 결정된다.

- 함수를 선언할 때 this를 사용할 수 있다. 다만, 함수가 호출되기 전까지 this엔 값이 할당되지 않는다.
- 함수를 복사해 객체 간 전달할 수 있다.
- 함수를 객체 프로퍼티에 저장해 object.method()같이 메서드 형태로 호출하면 this는 object를 참조한다.

화살표 함수는 자신만의 this를 가지지 않든다는 점에서 독특하다.
화살표 함수 안에서 this를 사용하면 외부에서 this값을 가져온다.



