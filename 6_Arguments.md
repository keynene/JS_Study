### Arguments
- Arguments : 전달받은 인자(매개변수)를 함수 내부로 전달하기 위해 사용되는 변수. (함수가 호출될 때의 인자 개수를 의미)
#예제1
>function sum(){
    var i, _sum = 0;
    for(i = 0; i < arguments.length; i++){
        console.log(i + ' : '+arguments[i]+ '\n');
        _sum += arguments[i];
    }
    return _sum;
}
console.log('result : ' + sum(1,2,3,4));

- sum이라는 함수를 선언할 때 매개변수 개수를 지정하지 않고 임의로 매개변수 지정 후 호출하면 성공적으로 실행됨
- arguemtns : 함수가 호출될 때의 매개변수를 저장 (1,2,3,4)
- arguemtns.length : 함수가 호출될 때의 매개변수 개수를 반환 (4개)


#예제2
>function one(arg1){
    console.log(
        'one.length', one.length + '\n',  → one이라는 함수의 파라미터 갯수
        'arguments.length', arguments.length  →실제 호출될 때의 아규먼트 갯수
    );
}
one('val1','val2');

- one.length : 함수가 선언될 때의 매개변수 개수를 의미 (1)
- arguemtns.length : 함수가 호출될 때의 매개변수 개수를 의미 (2)

※ 사용자가 필요 이상의 매개변수를 호출할 경우 에러창을 띄우는 등 응용가능!
if ( one.length != arguemnts.length){
	console.log('변수를 1개만 입력해주세요');
}