### Constructor
이전에 공부했었던 'new'를 통해 객체를 생성하는 생성자를 의미

#### constructor 사용 전
```javascript 
//noi 객체생성
var noi = {
    name:'noi',
    first:10,
    second:20,
    third:30,
    sum:function(){
        return this.first + this.second + this.third;
    }
}
//kim 객체생성
var kim = {
    name:'kim',
    first:10,
    second:10,
    third:10,
    sum:function(){
        return this.first + this.second + this.third;
    }
}
//각 객체 호출
console.log("noi.sum()", noi.sum()); //60
console.log("kim.sum()", kim.sum()); //30
```
- 코드가 길어지고 "불필요하고 의미없는 수정작업이 반복"됨


#### constructor 사용 후
```javascript
//noi, kim 객체 껍데기 함수 생성 (constructor)
function Person(name, first, second, third){
    this.name = 'kim';
    this.first = first;
    this.second = second,
    this.third = third,
    this.sum = function(){
        return this.first + this.second + this.third;
    }
}
//noi, kim 객체로 선언 및 매개변수로 객체 고유의 값 조정
var noi = new Person('noi', 10, 20, 30);
var kim = new Person('kim', 10, 10, 10);
console.log("noi.sum()", noi.sum()); //60
console.log("kim.sum()", kim.sum()); //30
```
- constructor를 사용함으로써 불필요한 반복작업이 제거되었고 코드가 줄었음
- 이후 수백, 수만개 객체를 생성하더라도 코드의 길이가 크게 길어지지 않을것이며, 반복작업할 필요가 없을 것임

> #### Constructor의 효용
> 1. 객체를 생성한다
> 2. 객체의 초기상태를 세팅한다
> 3. 객체 생성 시 무한사용이 가능하다
