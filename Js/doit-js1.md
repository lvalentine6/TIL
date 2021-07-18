JavaScript
==========

JavaScript란?
---------------
* 자바스크립트는 프론트엔드 개발 언어이며 정적인 웹 문서를 동작을 부여한다.   


* 현재 ES6 버전이 가장 널리 사용되지만 일부 브라우저에서는 ES5만 지원한다.   


* 이전의 자바스크립트는 클라이언트 컴퓨터에서만 작동하였으나 NodeJs를 사용하면 서버에서도 작동한다.   


내부 스크릡트 분리하기
----------------
 * HTML 내부에서 작성된 자바스크립트는 소스의 유지 보수와 손상 방지를 위해 외부로 분리하는것이 좋다.      

```
<script src = "js 파일경로"></script>
```

변수
------------

* 변수 선언은 var 키워드를 사용한다.


* 변수에 저장할 수 있는 자료형
	* 문자형(String)    
	* 숫자형(Number)     
	* 논리형(Boolean)     
	* Null & undefined = null은 변수에 저장된 값이 null인 경우이고 undefined는 변수의 값이 등록되기 전 상태

* typeof 를 사용하여 자료형을 알 수 있다.    

```
type of 변수 또는 데이터
```

연산자
-------------
* 복합 대입 연산자   

```
<script>

var a = 10;
var b = 2;

a += b; <- a는 a와 b를 더하고 대입한것
a -= b; <- a는 a와 b를 빼고 대입한것
a *= b; <- a는 a와 b를 곱하고 대입한것
a %= b; <- a는 a와 b를 나누고 대입한것

</script>
```

* 증감 연산자

```
var a = ++b; <- b의 값을 먼저 1증가하고 a에 그 값을 대입

var a = b++; <- a에 b의 값을 먼저 대입하고 그 뒤에 값을 1만큼 증가
```

* 비교 연산자

```
a == b <- 숫자를 비교할 경우 자료형을 따지지 않고 숫지만 일치하면 true 반환

a != b <- 숫자를 비교할 경우 자료형을 따지지 않고 숫지만 일치하면 false 반환

a === b <- 숫자를 비교할경우 숫자와 자료형이 모두 일치해야만 true 반환

a !== b <- 숫자를 비교할경우 숫자와 자료형이 모두 일치하지 않아야 true 반환
```

* 연산자 우선순위

	1. () 
	2. 단항 연산자 (--, ++, !)
	3. 산술 연산자 (*, /, %, +, -)
	4. 비교 연산자 (>, <, == ''')
	5. 논리 연산자 (&&, ||)
	6. 대입 연산자 (=, +=, -= ''')

* 삼항 조건 연산자

```
조건식 ? 스크립트 코드1 : 스크립트 코드2;

var a = 10;
var b = 3;

var result = a > b ? "hi" : "hello"; -> hi 출력
```
