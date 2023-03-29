Websocket, JSON
=========

Websocket이란?
---------

- 웹소켓이란 서버와 클라이언트 간 효율적인 양방향 통신을 위한 통신 프로토콜이다.
    * ex): 실시간으로 정보를 주고 받아야 하는 채팅 등...
    * 실시간이란 내가 확인하지 않아도 나에게 정보가 올 수 있는 통신이다.
    * TCP를 기반으로 하며 HTTP보다 상위 형태로 통신이 진행된다.

작동원리
-------

- 서버와 클라이언트 첫 연결은 HTTP를 사용해서 연결을 시도한다.
- 그리고 연결이 정상적으로 이루어 졌다면 추가적으로 Websocket 연결을 시도한다.
- 페이지 다운로드가 완료되면 HTTP 연결은 종료되고 다른 페이지로 이동하기 전까지 Websocket 연결은 지속된다.

의존성
------

- Spring-websocket : 웹소켓 통신용 라이브러리
- jackson-databind : JSON 전송용 라이브러리

도구
------

* 웹소켓 서버를 구현하기 위해서는 특정 클래스를 상속받아야 한다.
    * interface WebSocketHandler
    * class TextWebSocketHandler

* 상속 이후에 아래 메소드를 재정의하여 사용자의 접속, 종료, 통신을 관리할 수 있다.
    * afterConnectionEstablished : 사용자 접속 직후에 실행되는 콜백 메소드
    * afterConnectionClosed : 사용자 접속 종료 직후에 실행되는 콜백 메소드
    * handleTextMessage : 메세지가 수신된 직후에 실행되는 콜백 메소드

JSON이란?
-------

- JSON이란 JavaScript Object Notation 약자로 속성-값 쌍 또는 키-값 쌍으로 이루어져 있다.
- JSON은 경량 형태의 DATA 교환 형식이다.
- JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서 XML 대체제로 많이 이용한다.
- 특정 언어에 종속되지 않으며 많은 언어에서 JSON 표현식을 핸들링 할 수 있는 라이브러리를 지원한다.
