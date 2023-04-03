Http3
-------------

### Http 상태코드

* 1xx(informational) : 요청이 수신되어 처리중 (거의 사용하지 않음)
* 2xx(Successful) : 요청 정상 처리
    * 200 OK : 요청 성공
    * 201 Create : 요청 성공해서 새로운 리소스가 생성됨 (header 필드에서 식별)
    * 202 Accepted : 요청이 접수되었으나 처리가 완료되지 않았음
    * 204 No Content : 서버가 요청을 성공했지만, 응답 페이로드에 본문에 보낼 데이터가 없음(웹 문서 편집기 save 버튼)
* 3xx(Redirection) : 요청을 완료하려면 추가 행동이 필요
    * 리다이렉션의 이해
        * 자동 리다이렉트 흐름 : 클라이언트 요청 -> 헤더에 바뀐 URL을 담아 3xx 응답 -> 클라이언트 바뀐 URL을 다시 요청 -> 서버 200 Ok 응답
        * 영구 리다이렉션 : 특정 리소스의 URI가 영구적으로 이동
            * 301 Moved Permanently : 원래의 URL을 사용하지 않음, 브라우저에서 변경 인지
            * 리다이렉트시 요청 메서드가 Get으로 변하고, 본문이 제거될수 있음
            * 308 Permanent Redirect : 301과 기능은 같음
            * 리다이렉트시 요청 메서드와 본문 유지
        * 일시 리다이렉션 : 일시적인 변경
            * 302 Found : 리다이렉트시 요청 메서드가 Get으로 변하고 본문이 제거될 수 있음
            * 307 Temporary Redirect : 302와 기능은 같음
            * 리다이렉트시 요청 메서드와 본문 유지(요청 메서드를 변경하면 안된다.)
            * 303 See Other : 302와 기능은 같음
            * 리다이렉트시 요청 메서드가 Get으로 변경
            * 일시 리다이렉트 예시
                * POST로 주문후에 웹 브라우저를 새로고침하면?
                * 새로고침은 다시 요청
                * 중복 주문이 될 수 있다.
                * __POST로 주문후에 주문 결과 화면을 GET 메서드로 리다이렉트__
            * 302 vs 307 vs 303
                * 302 : GET으로 변할수 있음
                * 307 : 메서드가 변하면 안됨
                * 303 : 메서드가 GET으로 변경
                * GET으로 변해도 된다면 그냥 302를 써도 무방하다
            * 304 Not modified : 캐시를 목적으로 사용
            * 클라이언트에게 리소스가 수정되지 않았음을 알려준다
            * 클라이언트는 로컬 PC에 저장된 캐시를 재사용한다.
            * 304 응답은 캐시를 사용해야 함으로 응답에 메시지 바디를 포함하면 안된다.
            * 조건부 GET, HEAD 요청시 사용
        * 특수 리다이렉션 : 결과 대신 캐시를 사용
* 4xx(Client Error) : 클라이언트 오류, 잘못된 문법등으로 서버가 요청을 처리할 수 없음
    * 클라이언드가 이미 잘못된 요청을 하고 있으므로 재시도 해도 실패함
    * 400 Bad Request : 요청 구문, 메시지 등등 오류
    * 클라이언트는 요청 내용을 다시 검토하고 보내야함
    * 401 Unauthorized : 인증 되지 않음
    * 401 오류 발생시 응답에 WWW_Authenticate 헤더와 함께 인증 방법을 설명
    * 인증 : 본인이 누구인지 확인(로그인)
    * 인가 : 권한부여 (ADMIN 권한같은)
    * 403 Forbidden : 서버가 요청을 이해했지만 승인을 거부함
    * 어드민 등급이 아닌 사용자가 로그인은 했지만, 어드민 등급의 리소스에 접근하는 경우
    * 404 Not Found : 요청 리소스가 서버에 없음 or 권한이 없을때 리소스를 숨기고자 할때
* 5xx(Sever Error) : 서버 오류, 서버가 정상적으로 요청을 처리하지 못함
    * 500 Server Error : 서버 문제로 오류 발생, 애매하면 500 오류처리
    * 503 Service Unavailable : 서비스 이용 불가
    * 서버가 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없음
    * Retry-After 헤더 필드로 얼마뒤에 복구되는지 보낼 수도 있음

### HTTP 헤더

* HTTP 헤더의 용도
    * HTTP 전송에 필요한 모든 부가정보
    * RFC2614(과거)
        * General 헤더 : 메시지 전체에 적용되는 정보
        * Request 헤더 : 요청 정보
        * Response 헤더 : 응답 정보
        * Entity 헤더 : 엔티티 바디 정보
            * 엔티티 헤더는 엔티티 본문의 정보
    * RFC7230~7235(현재)
        * 앤티티 -> 표현 = 표현 메타데이터 + 표현 데이터
        * 메시지 본문을 통해 표현 데이터 전달
        * 메시지 본문 = 페이로드(payload)
        * 표현은 요청이나 응답에서 전달할 실제 데이터
        * 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
            * 데이터 유형(html, json), 데이터 길이, 압축 정보 등등
    * 표현
        * Content-Type : 표현 데이터의 형식
            * 미디어 타입, 문자 인코딩
            * text/htmt; charset=utf-8
        * Content-Encoding : 표현 데이터의 압축 방식
            * 표현 데이터를 압축하기 위해 사용
            * 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
            * 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
        * Content-Language : 표현 데이터의 자연 언어
            * 표현 데이터의 자연 언어 (en, kr)
        * Content-Length : 표현 데이터의 길이
            * 바이트 단위
    * 협상(컨텐츠 네고시에이션)
        * 클라이언트가 선호하는 표현 요청
        * Accept: 클라이언트가 선호하는 미디어 타입 전달
            * Accept-Charset: 클라이언트가 선호하는 문자 인코딩
            * Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
            * Accept-Language: 클라이언트가 선호하는 자연 언어
            * 협상 헤더는 요청시에만 사용
        * 협상과 우선순위 1
            * Quality Values(q) 값 사용
            * 0~1, 클수록 높은 우선순위
            * 생략하면 1
            * Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
            * 1st : ko-KR;q=1 (q생략)
            * 2st : ko;q=0.9
            * 3st : en-US;q=0.8
            * 4st : en:q=0.7
        * 협상과 우선순위 2
            * 구체적인 것이 우선한다.
            * Accept: text/*, text/plain, text/plain;format=flowed, */*
                * 1st : text/plain;format=flowed
                * 1st : text/plain
                * 1st : text/*
                * 1st : */*
        * 협상과 우선순위 3
        * 구체적인 것을 기준으로 미디어 타입을 맞춘다.
            * Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1,
              text/html;level=2;q=0.4, */*;q=0.5
* 전송 방식
    * 단순 전송
    * 압축 전송
    * 분할 전송
    * 범위 전송
* 일반 정보
    * From : 유저 에이전트의 이메일 정보
        * 일반적으로 잘 사용되지 않음
        * 검색 엔진 같은곳에서 주로 사용
        * 요청에서 사용
    * Referer : 이전 웹 페이지 주소
        * 현재 요청된 페이지의 이전 웹 페이지 주소
        * A -> B로 이동하는 경우 B를 요청할 때 Referer: A 를 포함해서 요청
        * Referer를 사용해서 유입 경로 분석 가능
        * 요청에서 사용
        * 참고: referer는 단어 referrer의 오타
    * User-agent : 유저 에이전트 애플리케이션 정보
        * user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/
          537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
        * 클리이언트의 애플리케이션 정보(웹 브라우저 정보, 등등)
        * 통계 정보
        * 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
        * 요청에서 사용
    * Server : 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
        * Server: Apache/2.2.22 (Debian)
        * server: nginx
        * 응답에서 사용
    * Date : 메시지가 발생한 날짜와 시간
        * Date: Tue, 15 Nov 1994 08:12:31 GMT
        * 응답에서 사용
* 특별한 정보
    * Host : 요청에서 사용하며 필수
        * 하나의 서버가 여러 도메인을 처리해야 할 때
        * 하나의 IP주소에 여러 도메인이 적용되어 있을 때
    * Location : 페이지 리다이렉션
        * 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동
          (리다이렉트)
        * 응답코드 3xx에서 설명
        * 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
        * 3xx (Redirection): Location 값은 요청을 자동으로 리디렉션하기 위한 대상 리소스를
          가리킴
    * Allow : 허용 가능한 HTTP 메서드
        * 405 (Method Not Allowed) 에서 응답에 포함해야함
        * Allow: GET, HEAD, PUT
    * Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
        * 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
        * Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
        * Retry-After: 120 (초단위 표기)
    * Authorization : 클라이언트 인증 정보를 서버에 전달
        * Authorization: Basic xxxxxxxxxxxxxxx
    * WWW-Authenticate : 리소스 접근시 필요한 인증 방법 정의
        * 리소스 접근시 필요한 인증 방법 정의
        * 401 Unauthorized 응답과 함께 사용
        * WWW-Authenticate: Newauth realm="apps", type=1,
          title="Login to \"apps\"", Basic realm="simple"
* 쿠키
    * Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
    * Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달
    * Stateless
        * HTTP는 무상태(Stateless) 프로토콜이다.
        * 클라이언트와 서버가 요청과 응답을 주고 받으면 연결이 끊어진다.
        * 클라이언트가 다시 요청하면 서버는 이전 요청을 기억하지 못한다.
        * 클라이언트와 서버는 서로 상태를 유지하지 않는다.
    * 클라이언트가 먼저 쿠키 저장소를 탐색 -> 없으면 user 정보를 함께 전송 -> 서버에서 set-Cookie로 응답 -> 클라이언트 쿠키 저장소에 저장됨
    * 쿠키 예시
        * 예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
        * 사용처
            * 사용자 로그인 세션 관리
            * 광고 정보 트래킹
        * 쿠키 정보는 항상 서버에 전송됨
            * 네트워크 트래픽 추가 유발
            * 최소한의 정보만 사용(세션 id, 인증 토큰)
            * 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 (localStorage, sessionStorage) 참고
        * 보안에 민감한 데이터는 저장하면 안됨(주민번호, 신용카드 번호 등등)
    * 쿠키 생명 주기
        * Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
        * 만료일이 되면 쿠키 삭제
        * Set-Cookie: max-age=3600 (3600초)
        * 0이나 음수를 지정하면 쿠키 삭제
        * 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
        * 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지
    * 쿠키(domain) - 도메인
        * 예) domain=example.org
        * 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
            * domain=example.org를 지정해서 쿠키 생성
            * example.org는 물론이고
            * dev.example.org도 쿠키 접근
        * 생략: 현재 문서 기준 도메인만 적용
            * example.org 에서 쿠키를 생성하고 domain 지정을 생략
            * example.org 에서만 쿠키 접근
            * dev.example.org는 쿠키 미접근
    * 쿠키(path) - 경로
        * 예) path=/home
            * 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
            * 일반적으로 path=/ 루트로 지정
        * 예)
            * path=/home 지정
            * /home -> 가능
            * /home/level1 -> 가능
            * /home/level1/level2 -> 가능
            * /hello -> 불가능
    * 쿠키 - 보안(Secure, HttpOnly, SameSite)
        * Secure
            * 쿠키는 http, https를 구분하지 않고 전송
            * Secure를 적용하면 https인 경우에만 전송
        * HttpOnly
            * XSS 공격 방지
            * 자바스크립트에서 접근 불가(document.cookie)
            * HTTP 전송에만 사용
        * SameSite
            * XSRF 공격 방지
            * 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송
* 캐시
  * 캐시는 자주 사용되는 리소스를 클라이언트에 저장하여 불필요한 리소스 요청을 줄이는 것이다.
  * 만약 캐시가 없다면 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드 받아야 한다.
  * 클라이언트가 리소스 요청시 서버는 HTTP 헤더에 캐시 유효시간을 담아 응답한다.
  * 만약 유효시간이 지났다면 클라이언트는 서버에 다시 리소스를 요청한다.
  * 그러나 만약 리소스의 변화가 없다면 이 때 불필요하게 다시 리소스를 받게된다.
  * 따라서 검증 헤더를 사용하여 리소스가 변경되었을 때만 리소스를 다시 요청하는 방식으로 동작한다.
  * 리소스가 변경되지 않았다면 서버는 304 Not Modified + 헤더 메다 정보로만 응답한다.
  * 클라이언트는 서버의 응답 헤더 정보로 캐시의 메다 정보를 갱신한다.
  * 검증 헤더와 조건부 요청
    * 검증 헤더
      * 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
      * Last-Modified, ETag
    * 조건부 요청 헤더
      * 검증 헤더로 조건에 따른 분기이다.
      * If-Modified-Since : Last-Modified 사용 (UTC를 이용한 날짜 시간 응답)
      * If-None-Match : ETag 사용
      * 조건을 만족하면 200 OK 응답
      * 조건을 만족하지 않으면 304 Not Modified
    * Last-Modified, If-Modified-Since의 단점
      * 1초미만 단위로 캐시 조정이 불가능
      * 날짜 기반의 로직 사용
      * 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 결과가 똑같은 경우
      * 서버에서 별도의 캐시 로직을 관리하고 싶은 경우
    * ETag(Entity Tag)
      * 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
        * ex : ETag "v1.0"
      * 데이터가 변경되면 이 이름을 바꾸어서 변경함(Hash를 다시 생성)
      * 클라이언트는 ETag만 보내서 같다면 리소스를 유지하고, 다르다면 다시 리소스를 요청한다.
      * 캐시 제어 로직을 서버에서 완전히 관리
      * 클라이언트는 캐시 매커니즘을 모르게 된다.
    * 캐시 제어 헤더
      * Cache-Control : 캐시 지시어
        * Cache-Control: max-age -> 캐시 유효 시간, 초 단위
        * Cache-Control: no-cache -> 리소스를 캐시를 허용하지만 항상 원 서버에 검증하고 사용
        * Cache-Control: no-store -> 데이터나 리소스에 민감한 정보가 있으므로 저장하면 안됨
        * Pragma: no-cache -> HTTP 1.0 하위 호환
        * Expires -> 캐시 만료일을 정확한 날짜로 지정
          * HTTP 1.0 부터 사용
          * 지금은 더 유여한 Cache-Control: max-age를 권장
          * 만약 Cache-Control: max-age와 함께 사용한다면 Expires는 무시된다.
  * 프록시 캐시
    * 요청과 응답 시간을 줄이고자 프록시 캐시 서버를 사용한다.
    * 프록시 서버에는 public 캐시가 저장되고, 클라이언트에는 private 캐시가 저장된다.
      * Cache-Control: public
        * 응답이 public 캐시에 저장되어도 됨
      * Cache-Control: private
        * 응답이 해당 사용자만을 위한 것임, private 캐시에 저장해야 함(기본값)
      * Cache-Control: s-maxage
        * 프록시 캐시에만 적용되는 max-age
      * Age: 60 (HTTP 헤더)
        * 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)
  * 캐시 무효화
    * Cache-Control: no-cache
      * 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용(이름에 주의!)
    * Cache-Control: no-store
      * 데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)
    * Cache-Control: must-revalidate
      * 캐시 만료후 최초 조회시 원 서버에 검증해야함
      * 원 서버 접근 실패시 반드시 오류가 발생해야함 - 504(Gateway Timeout)
      * must-revalidate는 캐시 유효 시간이라면 캐시를 사용함
    * Pragma: no-cache
      * HTTP 1.0 하위 호환
