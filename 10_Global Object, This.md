### Global Object
- Global Object(전역객체) : window, global 등 global scope 내 항상 존재하는 객체
#window/global
- window : 브라우저 환경 전역객체 === global : 자바스크립트 환경 전역객체 
- '브라우저 탭'에 존재하는 자바스크립트의 전역 최상위 객체 (window로 어디서든 접근 가능)
- 전역으로 선언되어 있기 떄문에 window객체를 참조하지 않고도 property 이름으로 바로 접근 가능 (window.property === property)
- window 객체 안에 document 객체가 존재하고, document에는 잠재적으로 보여질 수 있는 dom에 대한 정보가 저장되어있음 (window.document로 접근 가능)

#### this
- this는 자신이 속한 객체 또는 자신이 생성할 인스턴스를 가리키는 자기 참조 변수
- this를 통해 자신이 속한 객체 또는 자신이 생성할 인스턴스의 프로퍼티나 메소드를 참조할 수 있음
- this는 코드 어디서든 참조할 수 있음
- this는 가변적이며 함수를 어떻게 호출하느냐에 따라 this가 가리키는 대상(객체)이 달라짐
- this는 객체의 프로퍼티나 메소드를 참조하기 위한 자기 참조 변수이므로 일반적으로 객체의 메소드 내부 또는 생성자 함수 내부에서만 의미가 있음
- '함수'와 '객체'의 관계가 느슨한 자바스크립트에서 이 둘을 연결시켜주는 역할
#### ★ 함수가 누구의 객체인가에 따라 this값이(this가 가리키는 객체) 달라짐
#예제1 (global === this)
>function func(){
    if(global === this){
        console.log("global === this"); //전역객체와 this가 같은지 확인
    }
}
func();

- this는 js내 전역객체 global을 가리킴

#예제2 (property === this)
>var o = {
    func : function(){
        if(o === this){
            console.log("o === this");
        }
    }
}
o.func();

- 객체 안에서의 this는 전역객체가 아닌 해당 property를 가리킴


#### call, apply, bind
1. call
- call은 모든 함수에서 사용할 수 있고, this를 특정 값으로 지정하는 역할
- 함수를 호출하면서 call을 사용하고 this로 사용할 객체를 넘기면 해당 함수가 주어진 객체의 메소드인 것처럼 사용가능
2. apply
- 사용법은 call과 동일
- call은 매개변수를 직접 받는다면 apply는 매개변수를 '배열'로 받는다
3. bind
- 사용법은 call, apply와 동일
- 함수의 this 값을 영구적으로 바꿀 수 있음