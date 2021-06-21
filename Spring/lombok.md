lombok
======

lombok란?
------------
* java 기반에서 기계적인 코드 작성을 __어노테이션 기반__ 으로 코드를 자동으로 완성해주는 라이브러리이다.    
* ex): getter, setter, toString..... 을 변환     

lombok의 장점
------------
* 코드 자동 생성을 통한 편리함, 생산성 향상
* 코드의 가독성 향상과 유지보수에 용이하다.

lombok의 단점
------------
* 협업시 모든 팀원이 전부 lombok을 사용해야 한다.
* 많은 어노테이션 사용시 해석이 난해해진다.


lombok의 기능
------------
__어노테이션을 클래스 선언 상단에 위치시키면 모든 변수들에 적용되고 변수 이름 위에 위치시키면 해당 변수들만 적용된다.__      

* @Getter : Getter 메소드 생성             
* @Setter : Setter 메소드 생성         
* @AllArgsConstructor : 모든 변수를 사용하는 생성자를 자동완성    
* @NoArgsConstructor : 모든 변수를 사용하지 않는 기본 생성자를 자동완성   
* @RequiredArgsConstructor : 
* @EqualsAndHashCode : 클래스에 대한 equals 함수와 hashcode 함수를 자동생성      
* @ToString : ToString 메소드를 자동으로 완성    
* @Data : @ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor 를 모두 자동생성    
* @Builder : 해당 클래스 객체 생성에 Builder 패턴을 적용    

참고
--------
[Lombok이란? 및 Lombok 활용법](https://mangkyu.tistory.com/78)     