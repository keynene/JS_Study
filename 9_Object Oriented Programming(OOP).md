### Object Oriented Programming
 - 객체 지향 프로그래밍 : 좀 더 나은 프로그램을 만들기 위한 프로그래밍 패러다임으로 로직을 상태(state), 행위(behave)로 이루어진 객체로 만든느 것.
 - 재활용성을 높여줌 (재활용 용이하도록 '부품화'하는 것이 관건)
 - 추상화 / 부품화 / 인터페이스
 
#Javascript : prototype-based programming
 - OOP의 문법을 비슷하게 사용하는 함수형 언어
 - property(프로퍼티) : 객체 안의 변수
 - method(메소드) : 객체 안의 함수
 
 #사용예제

```javascript
 function Person(name){
    this.name = name;
    this.introduce = function(){
        return 'My name is '+this.name;
    }
}
var p1 = new Person('keynene');
console.log(p1.introduce()+'\n');
var p2 = new Person('Noi');
console.log(p2.introduce()+'\n');
```

 - new(생성자) : 객체선언 및 초기화 / class 존재x, 생성자는 함수일 뿐이고 new를 사용하면 객체를 생성함
 - 사용방법 : 함수(Person()) 선언 후 변수(p1,p2)에 함수를 넣을 때 함수 앞에 new를 사용
 ※ 'name'은 개별, 'introduce()'는 중복이므로 name만 입력받고 introduce()는 바로 실행되도록 설계