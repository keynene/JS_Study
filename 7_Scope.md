### Scope
- scope : 변수의 값이 어디부터 어디까지 유효한지 판단하는 범위
### Local scope / Global scope
>let say = 'Hello';
function greeting(){
	let name = 'keynene';
    return say + ' ' + name;
}
greeting();  → 'Hello keynene'
name; → Reference Error

- name : Local scope내 변수
- say : Global scope내 변수
- name은 greeting이라는 Local scope를 벗어나면 호출할 수 없음

### Function scope / Block scope
#### 1. Function scope
>for(var i = 0; i < 3; i++){
	console.log(i);
}
console.log('final : ', i);   → 'final : 3'

#### 2. Block scope
>for(let i = 0; i < 3; i++){
	console.log(i);
}
console.log('final : ', i);   → Reference Error

- var : 대표적인 function scope. 함수안에서만 접근하면 얼마든지 i 사용 가능
- let, const : block scpe. {}중괄호 block을 벗어나면 사용 불가능

