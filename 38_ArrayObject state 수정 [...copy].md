## 📖Array/Object state 수정
- ```let copy = [...state/object명]``` 문법 사용
- React에서 array/object를 state로 저장하고 set(변경)할 때 사용
- copy문법 말고 setArray/setObject(변경값)을 사용한 경우 **array/object의 원본값이 수정됨**
- array의 원본값을 수정하지 않고 복제하여 setArray를 진행해야 데이터 손실이 없기 때문에
   copy문법을 사용해야 함

### 📝let copy = [...state/object명]를 사용하여 array/object값 복제/수정
#### ✏️버튼을 클릭하여 arr의 0번째 값을 수정하는 예제
```javascript
let [arr, setArr] = useState(['0','2','3']);

function App(){
  <button onClick={()=>{
    let copy = [...arr];  //copy라는 변수에 arr배열을 저장
    copy[0] = '1';  //copy배열의 0번째 인자 1로 수정 (arr원본은 건드리지 않음)
    setArr(copy);  //setArr를 이용하여 arr에 copy배열 저장
  }}>arr수정</button>
}
```