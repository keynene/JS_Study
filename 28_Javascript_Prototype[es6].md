### Prototype
- 객체 속성의 초기모델/원형
- 객체에서 어떠한 속성을 무한생성하지않고 여러 개의 객체에서 이용가능한 속성의 형태
- 1선언 n사용으로, 자원낭비를 줄일 수 있음
- 프로토타입을 사용하지 않을 경우 비효율 : 객체를 생성할 때마다 함수/메소드를 무한생성해야 하므로 메모리/자원낭비가 심함

#### Prototype 사용예제
```javascript
// constructor 생성
function Person(name, first, second){
    this.name = 'kim';
    this.first = first;
    this.second = second;
}
// prototype으로 선언한 Person의 sum의 함수는 최초 1번만 실행됨
Person.prototype.sum = function(){
    return 'prototype : '+ this.first + this.second;
}

var noi = new Person('noi', 10, 20);
// noi의 속성 직접적 선언하면 prototype보다 우선적으로 실행됨
noi.sum = function(){
    return 'this : '+ this.first + this.second; 
}
var kim = new Person('kim', 10, 10);
console.log("noi.sum()", noi.sum());
console.log("kim.sum()", kim.sum());
```
- 위 예제에서 noi는 noi.sum함수를, kim은 prototype의 sum함수를 실행함
- 자바스크립트는 우선순위에 따라 함수/객체의 속성을 실행한다
  ※ 우선순위 : 객체의 직접적인 속성 → prototype 유무확인