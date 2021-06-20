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
	* __View__ : 뷰는 실제로 보여지는 부분 이며 모델을 이용해 렌더링을 한다.   
		* ex):  jsp와 같은 파일
	* __Controller__ : 컨트롤러는 사용자의 요청을 받고 응답을 주는 역할을 담당한다.   


MVC Model 1 아키텍처
-----------------
<img src="https://cphinf.pstatic.net/mooc/20180219_180/1519003368125BcfqV_PNG/1.png" width="650px" height="300px" alt="MVC 모델 아키텍처 1"></img><br/>

###### 출처 : 부스트 코스 (https://www.boostcourse.org/web316/lecture/16762?isDesc=false)

* 모델 1 구성요소
	* JSP
	* JavaBeans
	
* 모델 1 특징
	* 브라우저의 요청을 JSP가 받아 직접 JavaBeans를 이용해서 작업을 처리하고 클라이언트에게 반환     

* 모델 1의 장점
	* 구조가 단순하여 이해하고 사용하기 쉽다.
	
* 모델 1의 단점
	* JSP에서 프론트엔드 코드와 백엔드 코드가 혼합되어 책



MVC Model 2 아키텍쳐
-----------------
<img src="https://cphinf.pstatic.net/mooc/20180219_65/1519003382079lUcI5_PNG/2.png" width="650px" height="300px"  alt="MVC 모델 아키텍처 1"></img><br/>

###### 출처 : 부스트 코스 (https://www.boostcourse.org/web316/lecture/16762?isDesc=false)

* Spring MVC    
		* Model2 MVC 패턴을 지원하는 Spring Module
