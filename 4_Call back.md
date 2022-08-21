### Call back
- method(메소드) : 객체의 속성 값(value)으로 담겨진 함수 (객체로의 함수사용)

#값으로 변환 전
>var numbers = [20, 10, 9,8,7,6,5,4,3,2,1];
function sortfunc(a,b){
    console.log(a,b);
    if(a > b){
        return 1;
    } else if(a < b){
        return -1;
    } else {
        return 0;
    }
}
console.log(numbers.sort(sortfunc));

#값으로 변환 후
>var numbers = [20, 10, 9,8,7,6,5,4,3,2,1];
var sortfunc = function(a,b){
    return a-b;
}
console.log(numbers.sort(sortfunc));

- Ajax : 일반적인 웹 페이지 변경없이, 서버와 웹 브라우저가 내부적으로 통신하는 방법 (별도 다운로드 x, 비동기적 제어)