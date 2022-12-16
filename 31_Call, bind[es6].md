```javascript
var kim = {name:'kim', first:10, second:20}
var jang = {name:'jang', first:10, second:10}
function sum(key){
    return key + (this.first + this.second);
}
```
※ 상기 자바스크립트 코드를 모든 예제에 적용

### Call
>#### method.call(this에 대입될 값, method의 인자값)
>원래 정의되어있는 sum이라는 함수에 this값과 인자값을 할당하여 실행
```javascript
// this=kim, key=kimCall
console.log(sum.call(kim, 'kimCall ')); // kimCall 30
// this=jang, key=jangCall
console.log(sum.call(jang, 'jangCall ')); // jangCall 20
```

### Bind
>#### method.bind(새로 생성할 method의 this에 대입될 값, method 인자값)
>원래 정의되어있는 sum 함수를 복제한 새로운 함수에 this값, method 인자값 할당하여 저장
```javascript
var kimBind = sum.bind(kim, 'kimBind '); //kimBind 변수에 'kimBind'라는 인자값가진 sum함수 저장
console.log(kimBind()); // kimBind 30   (함수이므로 kimBind가 아닌 kimBind()로 호출)
```