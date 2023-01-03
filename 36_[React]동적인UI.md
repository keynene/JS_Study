## 📖동적인UI
 - 일반적으로 JSX는 **if / else** 문법을 쓸 수가 없음
 - **useState** 또는 **삼항연산자**를 이용하여 구현
 
 * * *
 
### 📝동적UI 구현 step
1. html css 코드로 컴포넌트 UI 구현
2. UI 현재상태 state로 저장 (string, int, boolean 다 가능)
3. state에 따라 UI가 어떻게 보일지 **조건문**으로 작성
4. **삼항연산자**를 사용하여 동적으로 작동하게 변경
👉🏻(React에서 JS코드는 **{ 중괄호 }**안에 작성하면 됨)

* * *

#### ✏️ 'MODAL' 문자 클릭 시 모달창이 여닫히는 예제
```javascript
//1. html, css 코드로 컴포넌트 UI 구현 (css는 생략)
function Modal(){
  return (
    <div className="modal">
      <h4>제목</h4>
      <p>날짜</p>
      <p>상세내용</p>
    </div>
  )
}
function App() {
  //2. UI현태상태지정 : true:열림 false:닫힘
  let [modal, setModal] = useState(false); 
  
  return (
    //3. MODAL문자와, 상태에 따라 UI가 어떻게 보일지 조건문 작성
    <h4 onClick={()=>{
          if(modal == false){
            setModal(true);
          } else {
            setModal(false);
          }
        }}>MODAL</h4>
   
   // 중괄호{}안에 JS코드 입력가능
   // React(HTML코드)에서는 if/else의 조건문은 불가능
   // 👉🏻삼항연산자를 사용해야 함

     //4. 삼항연산자를 이용하여 동적으로 변경
     //조건식 ? 참일 때 실행할 코드 : 거짓일 때 실행할 코드
   {
     modal == true ? <Modal/> : null
   }
)
```

* * *

#### 💡동작원리
현재 modal 변수의 상태를 **false(닫힘)** 으로 state에 저장해두고, 
h4태그 안의 "MODAL" 클릭 시 **setModal**로 modal의 상태를 true/false로 순차적으로 변경하여 
Modal 컴포넌트를 여닫음