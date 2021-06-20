MVC
========

MVC란?
-------------   
* __MVC란 Model-View-Controller__ 의 약자로 기본 시스템 모듈을 __MVC__ 로 나누어 구현된 것을 말한다.
* 원래는 제록스 연구소에서 일하던 트뤼그베 린즈커그가 처음으로 소개한 개념으로, 데스트톱 어플리케이션용으로 고안되었다.    
* 이것을 웹에 적용한 것이 __Web MVC__ 이다.    
	* __Model__ : 모델은 뷰가 렌더링하는데 필요한 데이터       
		* 렌더링 : 브라우저에게 뿌려질 화면을 만드는 과정       
		* ex):  상품 목록, 주문 내역      
	* __View__ : 뷰는 모델을 이용해 렌더링을 하며 실제로 보여지는 부분이다.    
		* ex):  jsp와 같은 파일
	* __Controller__ : 컨트롤러는 사용자의 요청을 받고 응답을 주는 역할을 담당한다.   


MVC Model 1 아키텍처
-----------------
<img src="https://cphinf.pstatic.net/mooc/20180219_180/1519003368125BcfqV_PNG/1.png" width="650px" height="300px" alt="MVC 모델 아키텍처 1"></img><br/>

###### 출처 : 부스트 코스 (https://www.boostcourse.org/web316/lecture/16762?isDesc=false)

* 모델 1 구성요소
	* JSP
	* JavaBeans or 서비스 클래스
	
* 모델 1 특징
	* 브라우저의 요청을 JSP가 받아 직접 JavaBeans를 이용해서 작업을 처리하고 클라이언트에게 반환     

* 모델 1의 장점
	* 구조가 단순하여 이해하고 사용하기 쉽다.
	
* 모델 1의 단점
	* JSP에서 프론트엔드 코드와 백엔드 코드가 혼합되어 코드가 복잡해지고 분업에 불편하다.    
	* 복잡한 코드로 유지보수가 어렵다.    



MVC Model 2 아키텍쳐
-----------------
<img src="https://cphinf.pstatic.net/mooc/20180219_65/1519003382079lUcI5_PNG/2.png" width="650px" height="300px"  alt="MVC 모델 아키텍처 1"></img><br/>

###### 출처 : 부스트 코스 (https://www.boostcourse.org/web316/lecture/16762?isDesc=false)

* 모델 2 구성요소
	* Servlet
	* JSP
	* JavaBeans or 서비스 클래스
	
* 모델 2 특징
	* 브라우저의 요청을 서블릿이 받아 제어한다. 요청에 대한 로직 처리는 모델인 자바빈이이 담당하고 요청 결과는 JSP가 담당하게 된다.

* 모델 2 장점
	* 뷰코드와 로직 처리를 위한 자바 코드의 분리로 JSP의 코드가 모델 1에 비해 간결하다.    
	* 분업이 용이하다.     
	* 기능에 따라 분리되어 있어 유지보수가 편리하다.     
	
* 모델 2 단점
	* 구조가 복잡하고 작업량이 많다.   
	
Spring MVC
-------------

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcAkzFN%2FbtqBp4AIlD3%2FmE8PbHZQh0WtvB0wqULb3k%2Fimg.png" width="650px" height="300px"  alt="Spring MVC 동작 흐름"></img><br/>

###### 출처 : 부스트 코스 (https://www.boostcourse.org/web316/lecture/16762?isDesc=false)

* Spring Framework에서 MVC Model2 아키텍쳐를 기반으로 제공하는 웹 모듈이다.         

* 가장 앞단에서 유저의 요청을 받는 컨트롤러를 프론트 컨트롤러라고 한다.        
	* DispatcherServlet 객체가 이 역할을 수행한다.         
	* 로직에 들어오기 전에 가장 먼저 작업을 수행한다.        
	* ex): 멀티파트 파일 업로드, 지역정보 결정     
	
* 프론트 컨트롤러는 요청을 어떤 핸들러가 처리해야 할지 매핑한다. (핸들러 매핑)      

* 매핑된 핸들러를 실제로 실행하는 역할을 핸들러 어댑터가 담당한다.       

* 컨트롤러는 해당 요청을 처리하는 로직을 담고있다.       
	* 내부적으로 Service 단위로 나누어 모듈화 한다.    
	* DB에 접근할 수 있는 Repository 객체를 이용해서 데이터에 접근할 수 있다.      
	
* 컨트롤러는 서비스에서의 로직 처리 후 결과를 뷰 리졸버를 거쳐 뷰 파일을 렌더링 하여 내보낸다.    
	*ViewResolver 객체가 이 역할을 담당한다.      

참고
---------
[JSP 모델1과 모델2, 그리고 MVC 패턴](https://hsp1116.tistory.com/9)
[부스트코스 Spring MVC](https://www.boostcourse.org/web316/lecture/16762?isDesc=false)
[스프링 MVC](https://dailyheumsi.tistory.com/159)