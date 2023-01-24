## 📖Lifecycle
- 컴포넌트는 생성/재렌더링/삭제 의 lifecycle을 가짐
  1. 생성 : mount
  2. 재렌더링 : update
  3. 삭제 : unmount
- 컴포넌트가 생성/제랜더링/삭제될 때마다 특정코드를 실행하는 기능을 
useEffect()라는 hoock을 사용하여 구현 가능


* * *

### 📝Lifecycle 구현방법
#### ✏️기존 Class 컴포넌트의 lifecycle 구현방법

```javascript
class lifecycle extends React.Component {
  componentDidMount(){
    //컴포넌트가 로드되고나서 실행할 코드
  }
  componentDidUpdate(){
    //컴포넌트가 업데이트 되고나서 실행할 코드
  }
  componentWillUnmount(){
    //컴포넌트가 삭제되기 전에 실행할 코드
  }
}
```


#### ✏️현재 Function 컴포넌트의 lifecycle 구현방법 (useEffect())
```javascript
/*useEffect()라는 훅을 사용해서 lifecycle을 구현함*/
import {useEffect} from 'react';

function lifecycle(){
  useEffect(()=>{
  	//컴포넌트 로드 & 업데이트 될 때마다 실행할 코드
    //react의 html코드를 다 로드하고 나서 실행됨 (로드지연 방지)
  }, []) 
  //[] : mount시 1회 실행, [변수명] : 변수명이 변경될 때마다 실행
  
  return (
  	/*아래참고*/
  )
}
```
* * *

### 📝useEffect 사용방법

1. **재렌더링마다 코드 실행**
	```useEffect(()=>{ 실행할코드 })```

2. **mount시 1회 코드 실행**
	```useEffect(()=>{ 실행할코드 }, [])```
3. **mount시 1회, 변수/함수 변경 시 계속 실행**
```javascript
	useEffect(()=>{
      state사용 코드
    }, [state명])
```

4. **컴포넌트 삭제 시 코드 실행** 
  : 중복제거 함수 구현 시 자주 사용 (**clean up function**)

```javascript
	useEffect(()=>{
  	  //코드실행순서 : 2
      실행할코드 //변수,함수 쌓임 (ex. setTimeout())
  	  return()=>{
        //코드실행순서 : 1
        useEffect안의 "실행할코드" 실행 전 실행할 코드
        //쌓인 변수,함수 삭제 (ex. clearTimeout())
  	  } 
	})
 ```


* * *

### ❓useEffect() 사용하는 이유
#### useEfect()가 필요한 경우
1. 오래걸리는 반복연산
2. 서버에서 데이터 가져오기
3. 타이머 기능 구현 등
   (**신속성 및 정확한 시간측정**이 필요한 기능들)
   
👉🏻 BUT, 이러한 기능들이 컴포넌트가 로드 &업데이트 될 때마다 실행되면
함수/변수 등이 너무 많이 쌓여버리므로 삭제해줄 필요가 있음!

#### clean up function

1. clean up function 
: useEffect() 내 함수/변수이 로드&업데이트 마다 동작하여 수백-수천개 쌓일 것을 대비하여 사용
2. 필요한 경우 (예) 
: 2초마다 동작하는 타이머가 있으면 useEffect()내에서 여러 번 실행되어 
여러 개 쌓여버릴 때가 있는데, 이런 기존 타이머를 제거해줌
```
useEffect()의 return() 안에 clean up function을 주로 사용함
ex) clearTimeout();
```


  * * *
  
### 📜예제

#### 📌예제1 : 랜더링 2초 후 없어지는 창
```javascript
import {useState, useEffect} from 'react';

function lifecycle(){
  (중략)

  let [time, setTime] = useState(true);
  
  /*lifecycle 함수 구현 부분*/
  useEffect(()=>{
    //2초후 setTime(false)가 실행되는 함수를 timer 변수에 대입
  	let timer = setTimeout(()=>{ setTime(false) }, 2000)
    
    return()=>{
      //페이지가 랜더링 될 때마다 중첩되는것을 방지하기 위해 setTimeout()함수를 제거
      clearTimeout(timer); 
    }
  }, []) //랜더링 후 최초 1회만 실행
  
  /*react로 보여질 부분*/
  return (
    {
      time == true ?
      	<div>이 창은 2초 후 닫힙니다.</div>
      : null
    }
  )
}
```

* * *

#### 📌예제2 : 입력값이 숫자가 아닌경우 경고창 띄우기
```javascript
import {useState, useEffect} from 'react';

function lifecycle(){
  
  let [num, setNum] = useState('');
  
  /*lifecycle 함수 구현 부분*/
  useEffect(()=>{
  	if (isNaN(num) == true){
      alert('숫자만 입력하라니까!');
    }
  },[num]) //num이 변경될 때마다 실행
  
  
  /*react로 보여질 부분*/
  return(
    //input 창에 입력할 때마다 onChange안의 함수 실행
  	<input onChange=((e)=>{ setNum(e.target.value) }) />
  )
}
```

* * *

### 📚정리
1. **lifecycle**
  : 컴포넌트는 생성/재렌더링/삭제 사이클을 가짐

2. **useEffect()**
  : function 컴포넌트에서 로드&업데이트 시 실행되는 함수

3. **useEffect() 사용하기 좋은 예**
  : mount시 1회 코드 실행 👉🏻 useEffect()
  : 컴포넌트 삭제 시 코드 실행 👉🏻 useEffect()의 return()
  : clean up function 👉🏻 useEffect()의 return()
  : 1회 실행 + 변수/함수 변경될 때마다 실행 👉🏻 useEffect()의 [변수/함수]