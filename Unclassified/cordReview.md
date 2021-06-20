파이널 프로젝트 코드 리뷰 가이드
================================

코드 리뷰란?
------------

작업한 코드에 대해 팀원들과 코드에 대한 궁금한점 개선점등을 논의 하는것입니다.     
코드에 대해 설명하며 자신의 실력을 향상 시키고 타인의 코드를 이해하는 능력을 키울수 있습니다.    

파이널 프로젝트에서 코드리뷰가 필요한 이유
---------------------
* 기능들을 구현하기 전 명확한 기능 설계가 필요하다.       
		- 코드 리뷰를 통해서 추후 수정을 최소화할 수 있다.     
* 남의 코드나 구현한 기능들을 이해하기 어렵다.      
		- 코드 리뷰를 통해서 내가 직접 구현하지 않은 기능들도 어느정도 이해할 수 있다.      
* 다른 사람들과 나의 목표점이 다르다.        
		- 코드 리뷰를 통해 목표점을 협의하고 통일성 있는 결과물을 만들어 낼 수있다.    
* 코드 리뷰를 통해 자신의 실력을 키울수 있다.     
		- 나의 코드를 누군가에게 설명하기 위해 주석처리와 로직에 대한 설명을 꼼꼼히 하게된다.         
		- 타인의 코드에서 본받을점을 찾게된다.    

코드 리뷰 용어 정리
-------------------
 * <pre><code>CL</code></pre> Changelist의 약어로 버전 관리(Version Control)에 제출되었거나 코드 리뷰가 진행 중인 독립된 변경 단위입니다.                 
 * <pre><code>LGTM</code></pre> Looks Good to Me의 약어입니다. 위의 코드 리뷰를 승인할 때, 리뷰어가 사용합니다.        
 * <pre><code>Nit:</code></pre> 리뷰어들은 항상 무엇인가 더 나은 방법이 있을 수 있다는 의견을 자유롭게 남길 수 있어야 합니다.     
    그러나 그것이 그다지 중요하지 않다면 “Nit:”와 같은 접두어를 붙여 코드 작성자가 선택할 수 있도록 해야 합니다.        
 * <pre><code>PR</code></pre> Github의 협업 방식과 관련된 Pull Request를 의미합니다.      
 

제안하는 코드리뷰 진행법
----------------
1. 깃허브 래포지토리를 오픈 프로젝트로 생성하고 각자 브랜치 만들기      
2. 코드 작성 후 최소 단위로 끊어서 자신의 브랜치로 커밋     
		- 커밋 메시지    
		- 변경된 내용    
		- 변경이 필요한 이유와 결과     
3. 그 날 하루의 작업이 끝나면 main에 PR후 단톡방에 공유      
4. 최소 한명의 리뷰어가 최소 한개의 질문을 코멘트로 남기기     
5. 최소 한명의 리뷰어가 승인 하면 main에 병합      

참고 자료
-----------
* [GitHub 사용자 교육 코드리뷰](https://githubkorea.tistory.com/91)
* [구글 개발자 Code Review 가이드 번역본](https://wnsgml972.github.io/devops/2020/05/17/CodeReview1/)