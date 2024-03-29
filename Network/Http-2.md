Http2
-----------

* URI
    * URI (Uniform Resource Identifier)
        * URI는 로케이터, 이름, 또는 둘 다 추가로 분류될 수 있다.
        * 리소스를 식별하는 식별하는 통일된 방식
        * URI는 URL과 URN을 모두 포함하는 상위 개념
    * URL (Uniform Resource Identifier), URN (Uniform Resource Name)
        * URL - Locator : 리소스가 있는 위치를 지정
        * URN - Name : 리소스에 이름을 부여
        * URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
    * URL 구조
        * scheme://[userinfo@]host[:port][/path][?query][#fragment]
        * scheme : 주로 프로토콜에 사용한다. (http, https, ftp)
            * http는 80, https는 443을 주로 사용하며 생략이 가능하다.
        * userinfo : URL에 사용자 정보를 포함해서 인증하지만 거의 사용하지 않는다.
        * host : 도메인명이나 IP주소를 사용할 수 있다.
        * port : 접속 포트이며 생략 가능하다.
        * path : 리소스의 계층적 구조를 나타낸다. (item/iphone13)
        * query : key : value의 형태로 ?로 시작하고 & 이용하여 파라미터를 추가 가능하다.
        * fragment : html 내부 북마크 등에 사용하며 서버에 전송하는 정보가 아니다.
* 웹 브라우저 요청 흐름
    * DNS 조회 -> 브라우저가 HTTP 요청 메시지 생성 -> SOCKET 라이브러리를 통해 전달 -> TCP/IP 패킷 생성 HTTP 메시지 포함 -> 서버 수신
      -> 서버에서 HTTP 응답 메시지 생성 -> 클라이언트 수신 -> 브라우저 해석 -> 랜더링
* 모든것이 HTTP
    * HTML, TEXT, 이미지, 음성, 영상 파일, JSON, XML, 거의 모든 형태의 데이터 전송 가능
    * 서버간 데이터를 주고 받을때도 HTTP를 사용한다.
    * HTTP 1.1을 가장 많이 사용하며 HTTP2는 성능 개선, HTTP3은 UDP 사용하며 성능 개선
    * TCP : HTTP/1.1, HTTP/2
    * UDP : HTTP/3
    * HTTP 특징
        * 클라이언트 - 서버 구조
            * 클라이언트는 서버에 요청을 보내고 응답을 기다린다.
        * 무상태 프로토콜(stateless), 비연결성
            * 서버가 클라이언트 상태를 유지하지 않음
            * stateful - stateless 차이 : 노트북 구매 예시
            * stateful : 중간에 다른 점원으로 바뀌면 안된다. (다른 점원으로 바뀐다면 상태 정보를 미리 알려줘야 함)
            * stateless : 중간에 다른 점원으로 바뀌어도 되기에 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
            * 응답 서버를 쉽게 바꿀수 있어 무한한 서버 증설이 가능하다.
            * 서버에게 필요한 정보를 전부 담아서 요청해야 함
            * stateless 실무 한계
                * 모든것을 무상태로 설계하기는 힘들다.
                * 로그인한 사용자가 로그인 했다는 상태를 서버에 유지해야 할때
                * 일반적으로 브라우저의 쿠기와 서버 세션을 사용해서 상태 유지
                * 상태 유지는 최소한만 사용
            * 비연결성
                * 연결을 유지하지 않는다면 최소한의 자원만을 사용해 효율적이다.
                * HTTP는 기본적으로 연결을 유지하지 않는다.
                * 비연결성의 단점
                    * TCP/IP 연결을 새로 맺어야 함 -> 3 way handshake 시간 추가
                    * HTML + CSS + JS등 수많은 자원이 함께 다운로드 되기 때문에 효율적이지 않음
                    * HTTP 지속 연결 : 필요한 리소스를 전부 받기 전까지는 연결 유지
        * HTTP 메시지
        * ![http구조](https://user-images.githubusercontent.com/77956808/219685206-05e226f6-f46e-4250-a962-b042ea558a14.png)
        * 단순하며 확장 가능
* HTTP 메서드
    * HTTP API 만들기
        * URI 설계 : 회원 자체가 리소스가 된다. -> URI는 리소스만 식별함으로 리소스와 행위를 분리
        * 회원 목록 조회 -> /members
        * 회원 조회 -> /members/{id}
        * 회원 등록 -> /members/{id} -> 어떻게 구별하지?
        * 회원 수정 -> /members/{id}
        * 회원 삭제 -> /members/{id}
    * HTTP 메서드 상세
        * GET : 리소스 조회 -> 서버에 전달하고 싶은 데이터는 쿼리 파라미터를 통해서 전달, 메시지 바디를 사용할 수 있지만 지원하지 않는곳이 많아서 권장하지 않음
        * POST : 요청 데이터 처리, 주로 등록에 사용 -> 메시지 바디를 통해 서버로 요청 데이터 전달하고 모든 데이터 처리 가능
            * 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 함
            * 주요 POST 사용 -> 새 리소스 생성, 요청 데이터 처리(생성, 변경, 프로세스 처리), 다른 메서드로 처리하기 애매한 경우
        * PUT : 리소스를 __완전히__ 대체(덮어씌움), 해당 리소스가 없으면 생성
            * 클라이언트가 리소스의 위치를 알고 URI를 지정함 <-> POST와 차이점
        * PATCH : 리소스 부분 변경
        * DELETE : 리소스 삭제
        * HEAD : GET과 동일하지만 메시지 부분을 제외하고 상태줄만 헤더만 반환
        * OPTION : 대상 리소스에 대한 통신 가능 옵션을 설명(주로 CORS에서 사용)
    * HTTP 메서드의 속성
        * ![http메서드속성](https://user-images.githubusercontent.com/77956808/219697396-c239cd4c-b01a-4ef0-916e-4ba9c001b075.png)
        * 안전(Safe Methods) -> 호출해도 리소스를 변경하지 않는다.
        * 멱등(Idempotent) -> 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다.
            * GET : 몇번 조회하든 같은 결과가 조회된다.
            * PUT : 결과를 대체하기 때문에 같은 요청을 여러번 해도 최종 결과가 같다.
            * DELETE : 결과를 삭제하기 때문에 같은 요청을 여러번 해도 최종 결과가 같다.
            * POST : 멱등x, 두 번 호출하면 같은 결제가 두번 됨
            * 활용 -> 자동 복구 메커니즘, 서버가 TIMEOUT으로 정상 응답을 못주었을때 같은 요청을 다시해도 되는지에 대한 판단 근거
            * 멱등은 외부 요인으로 중간에 리소스가 변경되는 것 까지는 고려하지 않음
        * 캐시가능(Cacheable)
            * 응답 결과를 캐시해서 사용해도 되는가?
            * GET, HEAD, POST, PATCH 캐시 가능
            * 그러나 실제로는 GET, HEAD 정도만 캐시로 사용한다.
            * POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데 구현이 쉽지 않다.
    * HTTP 메서드 활용
        * 클라이언트에서 서버로 데이터 전송 방법
            * 쿼리 파라미터를 통한 데이터 전송
                * GET, 주로 정렬 필터(데이터)
            * 메시지 바디를 통한 데이터 전송
                * POST, PUT, PATCH
                * 회원 가입, 상품 주문, 리소스 변경, 등록
                  ![폼데이터전송](https://user-images.githubusercontent.com/77956808/219703637-ad8c8f67-9309-4ca3-a0fa-82e26e765156.png)
                  ![API전송](https://user-images.githubusercontent.com/77956808/219703670-8fa407fe-a8f0-4253-80a0-38ede0f73a9e.png)

    * HTTP 메서드 설계 예시
        * HTTP API - 컬렉션
            * POST 기반 등록
            * 서버가 리스스 URI 결정
        * HTTP API - 스토어
            * PUT 기반 등록
            * 클라이언트가 리소스 URI 결정
        * HTML FORM 사용
            * 순수 HTML + HTML FORM 사용
            * GET, POST만 지원
    * URI 설계 개념
        * 문서(document)
            * 단일 개념(파일 하나, 객체 인스턴스, 데이터베이스 row)
            * 예) /members/100, /files/star.jpg
        * 컬렉션(collection)
            * 서버가 관리하는 리소스 디렉터리
            * 서버가 리소스의 URI를 생성하고 관리
            * 예) /members
        * 스토어(store)
            * 클라이언트가 관리하는 자원 저장소
            * 클라이언트가 리소스의 URI를 알고 관리
            * 예) /files
        * 컨트롤러(controller), 컨트롤 URI
            * 문서, 컬렉션, 스토어로 해결하기 어려운 추가 프로세스 실행
            * 동사를 직접 사용
            * 예) /members/{id}/delete
