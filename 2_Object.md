### 객체구성
>var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
    for(key in grades){
        document.write("key : "+key+" / value : "+grades[key]+"<br />");
    }
    
 #for in 반복문 : for(key in object) → object안의 key값 차례로 반복
- 객체구성 : {key1 : value1, key2 : value2 ....}
- key값 호출 : document.write(key);
- value값 호출 : document.write(object[key]);