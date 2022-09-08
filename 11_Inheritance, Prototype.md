### Inheritance
- Inheritance(상속) : 객체는 연관된 로직들로 이루어진 작은 프로그램으로, 상속은 객체의 로직을 그대로 물려받는 또 다른 객체를 만들 수 있는 기능을 의미함
- 기존의 로직을 수정/추가 및 변경하여 파생된 새로운 객체를 만듦(객체응용)
- original 코드 변경으로 상속받는 자식객체에 동시다발적으로 동일하게 변경 가능
#활용예제
>function Person(name){    → 부모객체로 사용될 예정, 중복되는 코드 반영
    this.name = name;
}
Person.prototype.name = null;    
Person.prototype.introduce = function(){
    return 'My nickname is '+this.name;
}
function Programmer(name){   → 상속받을 자식1 프로그래머
    this.name = name;
}
Programmer.prototype = new Person();
Programmer.prototype.coding = function(){    → 프로그래머만의 요소 추가
    return "hello world";
}
function Desinger(name){   → 상속받을 자식2 디자이너
    this.name = name;
}
Desinger.prototype = new Person();
Desinger.prototype.design = function(){    → 디자이너만의 요소 추가
    return "beautiful";
}
////
var p1 = new Programmer('keynene');
console.log(p1.introduce()+'\n');
console.log(p1.coding()+'\n');
////
var p2 = new Desinger('Noi');
console.log(p2.introduce()+'\n');
console.log(p2.design()+'\n');


### Prototype
- Prototype(프로토타입)은 객체의 원형이라고 할 수 있음
- 함수는 객체이고, 생성자로 사용될 함수도 역시 객체임. 객체는 프로퍼티를 가질 수 있는데 prototype이라는 프로퍼티는 그 용도가 약속되어 있는 특수한 프로퍼티
- prototype에 저장된 속성들은 생성자를 통해 객체가 만들어질 때 그 객체에 연결됨
#Prototype Chain 예제
>function Ultra(){}
Ultra.prototype.ultraProp = true;  →key : UltraProp, value : true인 객체를 선언한 것이라고 할 수 있음 (자식에게 상속하기 위해 prototype 이용)
////
function Super(){}
Super.prototype = new Ultra();    →Super에 Ultra 속성들 상속
////
function Sub(){}
Sub.prototype = new Super();    →Sub에 Super 속성들 상속
////
var o = new Sub();    →o에 Sub 객체 생성
console.log(o.ultraProp);    →최종적으로 Sub도 Ultra의 속성 반환 가능
 1. 객체 o에서 ultraProp를 찾는다
 2. 없다면 Sub.prototype.ultraProp를 찾는다.
 3. 없다면 Super.prototype.ultraProp를 찾는다.
 4. 없다면 Ultra.prototype.ultraProp를 찾는다.
 ※ 선언된 객체에서 가장 가까운 곳의 부모객체 순으로 프로퍼티를 찾는다.