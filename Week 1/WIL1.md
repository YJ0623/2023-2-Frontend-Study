1장: JS 소개 - 생략

2장: 프로그램 작성법과 실행법 - 생략

3장: 변수와 값
-변수: 값을 담는 상자
-선언: var
-예약어: 변수로 사용 금지 단어
-데이터 타입: 원시 타입/객체 타입
-원시 타입: 숫자, 문자열, 논리값, null, undefined, Symbol 등..
-객체 타입: 객체
-숫자: int형, long형 등 존재 x. 오직 double타입에 해당
-심벌: 자기 자신을 제외한 그 어떤 값과도 다른 유일무이한 값.

ex) 
var sym1= Symbol();
var sym2= Symbol();
console.log(sym1==sym2) => "false"출력

4장: 객체와 배열, 함수의 기초
-객체: 데이터 여러 개를 하나로 모은 복합 데이터(연관 배열, 사전)

-ex)객체 리터럴로 객체 생성하기
var card = {suit: "하트", rank = "A"};
이때 suit와 rank는 프로퍼티의 이름, 하트와 A는 프로퍼티의 값

-ex)객체 리터럴 예제
var circle= {
    center:{x: 1.0, y: 2.0},
    radius: 2.5
};

-메서드: 프로퍼티에 저장된 값의 타입이 함수일 때, 그 프로퍼티를 메서드라 칭함.
-객체는 참조 타입임

-함수: 입력값="인수", 출력값="반환값"
ex)함수 선언문으로 함수 정의하기
function dist(p, q){
  var dx=q.x-p.x;
  var dy=q.y-p.y;
  return Math.sqrt(dx * dx + dy * dy);
};

-let: 블록 유효 범위를 갖는 지역 변수
-const: 블록 유효 범위를 가지면서 한 번만 할당할 수 있는 변수(상수)

-ex)함수 리터럴로 함수 정의하기
var square = function(x) {return x * x;};
-객체의 메서드: 객체의 프로퍼티 중에서 함수 객체의 참조를 값으로 담고 있는 프로퍼티
ex)
var circle = {
  center: {x:1.0, y:2.0},
  radius = 2.5,
  area: function() {
    return Math.PI * this.radius * this.radius
  }
};
에서 area는 메서드

-생성자: new 연산자 사용하여 객체 생성

-this: 메서드 함수 안에서 사용하면 그 값이 인스턴스의 프로퍼티
ex)
function Circle(center, radius){
  this.center = center;
  this.radius = radius;
  this.area=function(){
    return Math.PI * this.radius * this.radius;
  };
}
var p = {x:0, y:0};
var c= new Circle(p,2.0);
console.log("넓이 = " + c.area()); //넓이 = 12.566...

-내장 생성자: 사용자 정의 생성자 외의, JS에 원래부터 존재하는 생성자

-Date생성자: 날짜와 시간을 표현하는 객체 생성
ex)
var now = new Date();
console.log(now);
var then = new Date(2008, 5, 10);//개월수는 0 ~ 11(Jan~Dec)
console.log(then);
var elapsed = now - then;
console.log(elapsed); //밀리초 단위 정수로 계산
->프로그램 실행에 걸리는 시간 측정을 밀리초 단위로 계산 가능

-Function생성자: 함수를 생성하는 내장 생성자
ex)
var 변수 이름 = new Function(첫 번째 인수, ..., n번째 인수, 함수 몸통);

-배열 리터럴로 생성하기
ex)
var evens = [2,4,6,8];
var various = [3.14, "pi", true, {x:1}, [2,4,6,8]];

-length 프로퍼티: 배열 요소의 최대 인덱스 값 + 1

-Array 생성자: 배열 생성 가능 ex)
var evens = new Array(2, 4, 6, 8); //[2,4,6,8] 생성
-push, delete키워드로 배열 요소 추가/삭제

5장: 표현식과 연산자
-표현식: 어떤 값으로 평가되는 것
-연산자: +, - 등 복잡한 표현식을 만드는 것

-문자열 연결
-'+': 피연산자가 모두 문자열이면 문자열로 연결/문자열로 변환 가능한 객체라면 다른 피연산자의 타입을 문자열로 변환 후 연결 
-String객체:ex)
var msgObj = new String("Everything is practice");
-문자열에 프로퍼티를 사용 시 자동으로 String객체로 변환됨. 이때 String객체는 래퍼 객체(일시적 생성)

-관계 연산자(boolean값 반환): 관계 연산자, 논리 연산자
-비트 연산자
-기타 연산자: typeof연산자, 조건 연산자, 쉼표 연산자, eval함수

-6장: 웹 브라우저에서의 입출력

-대화상자 표시하기: window객체의 메서드 alert, prompt, confirm
-console 객체의 메서드: dir, error, info, time, timeEnd, trace, warn

-이벤트 주도형 프로그램: 이벤트가 발생할 때까지 기다렸다가, 이벤트가 발생했을 때 작업 수행
-이벤트 처리기: 이벤트가 발생했을 때 실행되는 함수

-DOM: JS 등의 프로그램이 HTML 요소를 조작할 수 있게 하는 인터페이스
-DOM 객체: window, document, 요소 객체
ex:
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>시각을 콘솔에 표시하기</title>
  <script>
    function displayTime(){
      var d = new Date();
      console.log("현재 시각은 "+ d.toLocaleString() + " 입니다.");
    }
    //1. window 객체의 onload 프로퍼티에 함수를 저장
    //이 함수는 웹 브라우저가 문서(body에 있는 HTML코드)를 모두 읽어들인 이후 실행됨
    window.onload=function(){
      //2. input 요소의 객체 가져오기
      var button = document.getElementById("button");
      //3. input 요소를 클릭했을 떄 동작하는 이벤트 처리기 등록
      button.onclick = displayTime;
    };
  </script>
</head>
<body>
  <input type="button" value="click" id="button">
</body>
</html>

-DOM에서 이벤트 처리기를 등록하는 목적: HTML코드와 JS코드 분리

-타이머: setTimeout, setInterval, claerInterval 메서드

-HTML 요소의 innerHTML 프로퍼티로 읽고 쓰기:ex)
display.innerHTML=((now-startTime)/1000).toFixed(2);
: 요소 객체 display의 innerHTML 프로퍼티에 경과 시간을 대입, id 속성 값이 display인 HTML요소의 내용 갱신

-폼 컨트롤의 입력 값 읽기: input 요소 객체의 value 프로퍼티 사용

-document.write: 일반적으로 dom을 사용하여 html요소로 출력이 일반적이나, JS에서는 사용.
document.write("<p>오늘은 "+ month + "월 " + day+ "일 입니다. </p>");
는 즉, <body><p>오늘은 month월 day일 입니다</p></body>와 동일하다.

-canvas의 특징: 저수준 API
canvas객체의 렌더랑 컨텍스트를 가져와 그림을 그림
-canvas의 키워드: moveto, lineto, fill, clear, arc, arcTo, rect, ...

-7장: 제어 구문

-if/else문, switch문, while문, do/while문, for문, for/in문: C++와 매우 유사. 학습 완료했습니다