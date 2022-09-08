### Standard Built-in Object
 - 내장객체, 즉 자바스크립트가 기본적으로 가지고 있는 객체
#### Object
 - 객체의 가장 기본적인 형태를 가지고 있는 객체
 - 아무것도 상속받지 않는 순수한 객체
 - 데이터를 저장하는 그릇
 - 모든 객체가 사용할 수 있는 function을 가지고 있음
 
#### 예제1
```javascript
var arr = new Array('seoul', 'new york', 'ladarkh', 'pusan', 'Tsukuba');
function getRandomValueFromArray(arr){
    var index = Math.floor(arr.length*Math.random());
    return arr[index];
}
console.log(getRandomValueFromArray(arr));
```
- Math.random() : 0~1사이 소수를 랜덤으로 제공
- Math.floor : 소수점 아래 숫자 절삭하여 정수만 제공
※ arr가 Array인지 확인하기 어렵고 가독성이 떨어짐

#### 예제2 (예제1 스탠다드 오브젝트 사용)
```javascript
Array.prototype.random = function(){  
//Array 사용하므로써 random이 array에 속해있다는 것을 알기쉬움(가독성)
    var index = Math.floor(this.length*Math.random());  //this는 배열 객체 자체를 가리킴
    return this[index];
}
var arr = new Array('seoul', 'new york', 'Lanark', 'pusan', 'Tsukuba');
console.log(arr.random());
var arr2 = new ArrayBuffer(1);
console.log(arr2);
```
- Array : 배열을 만들기 위한 생성자 함수

#### 예제3 (Object를 사용하여 모든객체에서 사용할 수 있는 함수 만들기)
```javascript
Object.prototype.contain = function(needle){
    for(var name in this){
        if(this[name] === needle){
            return true;
        }
    }
    return false;
}
var o = {'name':'keynene', 'city':'changwon'};
console.log(o.contain('keynene')); 
var a = ['keynene','noi','nonung'];
console.log(a.contain('noi'));
```
- contain : 인자에 해당하는 값(value)이 객체에 있는지 확인

#### 예제4 (예제3의 Object확장의 위험(모든 객체에 영향을 주기 때문))
```javascript
Object.prototype.contain = function(needle){
    for(var name in this){
        if(this[name] === needle){
            return true;
        }
    }
    return false;
}
var o = {'name':'keynene', 'city':'changwon'};
var a = ['keynene','noi','nonung'];
for(var name in a){
    console.log(name);  // 0,1,2,contain
}
```
※ 이런 경우 a에 contain이 추가되어 출력됨 (Object가 전체 객체에 관여하기 때문!)

#### 예제5 (문제 해결)
```javascript
Object.prototype.contain = function(needle){
    for(var name in this){
        if(this[name] === needle){
            return true;
        }
    }
    return false;
}
var o = {'name':'keynene', 'city':'changwon'};
var a = ['keynene','noi','nonung'];
for(var name in a){
    // 해결방법 : 어떠한 객체가 자신의 고유한 프로퍼티를 가지고 있는지 확인(hasOwnProperty)
    if(a.hasOwnProperty(name)){;   // 자신의 고유한 프로퍼티 일경우 (true일경우) 출력
        console.log(name);
    }
}
```
- hasOwnProperty : 자신의 고유한 프로퍼티인지 확인 true/false