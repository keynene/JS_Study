### 배열선언/호출
>function get_members(){
return ['egoing', 'k8805', 'sorialgi', 'noi'];
    }
    members = get_members(); //호출시 memebers[0],membrs[1] ...
    for(var i = 0; i < members.length; i++){
       document.write(members[i].toUpperCase()+"<br />");
    }
    
- 배열선언 : 일반적으로 members['egoing', 'k8805', 'sorialgi', 'noi']로 선언
- 배열의 크기 : members.length → 4
- 배열호출 : 인자값으로 호출 → member[0] : 'egoing'
- 소문자 → 대문자 : .toUpperCase()

### 배열추가
>var li = ['a', 'b', 'c', 'd', 'e']
    li.push('f');  //꼬리에 1개 값 추가
    li = li.concat('g','h');  //꼬리에 여러개 값 추가
    li.unshift('z', 'x');  //머리에 여러개 값 추가
    li.splice(2,0,'B','C');  //splice(index,howmany,값 여러개)
    
- push : 꼬리에 1개 값 추가
- concat : 꼬리에 여러개 값 추가
- unshift : 머리에 여러개 값 추가
- splice(index,howmany,값) : 중간에 값 추가   'index'앞에 'howmany'만큼의 기존값을 삭제하고 '값'추가