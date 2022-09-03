### Apply
- Apply : 특정함수가 특정객체의 속성인 것처럼 활용 가능
>o1 = {val1:1, val2:2, val3:3};
o2 = {v1:10, v2:50, v3:100, v4:25};
function sum(){
    var _sum = 0;
    for(var name in this){
        _sum += this[name];
    }
    return _sum;
}
console.log(sum.apply(o1));  →6
console.log(sum.apply(o2));  →185

- sum이 o1과 o2의 객체인것처럼 활용하여 함수실행