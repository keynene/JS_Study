### Closure
- Closure : 내부함수가 외부함수의 맥락(context)에 접근하는 방식

#내부함수에서 외부함수의 변수 사용 예제
>function outter(){
    var title = 'coding  everybody';
    function inner(){
        console.log(title); 
    }
    inner();
}
outter();

#외부함수를 사용하지 않을 때 (외부함수가 죽었을 때) 내부함수에서의 외부함수 사용 예제
>function outter(){
    var title = 'coding everybody';
    return function(){
        console.log(title);
    }
}
var inner = outter();
inner();

- outter()는 호출되지 않지만 inner라는 변수에 저장되어서 outter return값 반환 가능

#private variable
 : 정의한 함수내 요소들을 다른 사용자 또는 함수가 변경할 수 없게 하는 방법 
 >function factory_movie(title){
    return {
        get_title : function (){
            return title;
        },
        set_title : function (_title){
            title = _title;
        }
    }
}
ghost = factory_movie('Ghost in the shell');  → 각 ghost, matrix변수에 factory~함수 저장
matrix = factory_movie('Matrix');
console.log(ghost.get_title());
console.log(matrix.get_title());
ghost.set_title('공각기동대'); → ghost에 저장된 함수의 title값만 변경
console.log(ghost.get_title());
console.log(matrix.get_title());
※ ghost의 title 값만 '공각기동대'로 변경됨 (matrix는 그대로 'Matrix')

- 상기 private variable 방법으로 원하는 변수에 저장된 함수의 요소만 변경 가능 (다른 함수에서 함부로 변경할 수 없게 가능)

#closure 실패 예제
>var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(){
        return i;
    }
}
for(var index in arr){
    console.log(arr[index]());
}

#상기 closure예제 수정
>var arr = []
for(var i = 0; i < 5; i++){
    arr[i] = function(id){
        return function(){
            return id;
        }
    }(i);
}
for(var index in arr){
    console.log(arr[index]());
}
