컴퓨터 시스템 구조
----------------

* CPU : 연산을 담당
    * mode bit : 0과 1의 값을 가지고 현재 OS의 상태를 알 수 있게 한다.
        * 0일때 os가 cpu 점유 가지고 모든 명령 실행가능
        * 1일때 사용자 프로그램이 cpu를 점유 제한된 명령 실행 가능
    * timer : 사용자 프로그램이 cpu를 계속 점유하는것을 방지하기 위함 (time sharing)
        * 운영체제가 사용자 프로그램에게 cpu 점유권을 넘겨줄때 지정된 시간값 세팅
        * 지정된 시간이 지나면 timer interrupt가 발생하여 cpu 점유권이 OS로 돌아옴
        * OS는 다른 사용자 프로그램에게 cpu 점유권을 넘겨줌
    * memory controller, device controller
        * 메모리, IO 디바이스 작업을 수행하고 동시 작업을 제어함

* 사용자 프로그램은 IO가 발생하게 되면 메모리 영역에 직접 접근할 수 없기 때문에 OS에 interrupt를 걸어 __system call__ 을 요청 (trep)
    * 사용자 프로그램이 IO 디바이스에 마음대로 접근하는것을 막고자 함
    * OS는 interrupt를 판단하고 적절한지 파악후 IO controller에 명령을 내림
    * 그리고 다른 사용자 프로그램에게 cpu 점유권을 넘김
    * IO controller가 작업을 끝내면 interrupt 검
    * OS는 결과를 요청한 프로그램 memory에 넣음
    * 현재 실행하고 있는 프로그램의 타이머가 아직 남았다면 다시 현재 실행 프로그램에게 cpu 점유권을 넘김
    * 실행이 끝나면 다시 원래 호출한 프로그램에게 cpu 점유권을 넘김

* OS는 다양한 interrupt를 처리하는 방법이 담긴 코드의 주소가 interrupt vector라 함
* interrupt vector를 통해 해당 interrupt를 처리하는 커널 함수인 interrupt handler에 접근

* synchronous IO (동기식 입출력)
    * 사용자 프로그램에서 IO가 발생하면 OS는 명령을 지시하고 응답을 기다리고 결과를 받아야 cpu를 다시 반환
        * IO가 끝날 때까지 cpu 낭비 발생
        * 매 시점 하나의 IO만 일어남

    * IO가 완료될 떄 까지 cpu를 다른 프로그램에게 넘기고 호출 프로그램을 대기줄에 세우는 방법도 있음

* asynchronous IO (비동기식 입출력)
    * IO가 발생하면 명령을 지시하고 결과를 기다리지 않고 cpu를 사용자 프로그램에게 반환 cpu는 결과에 영향을 받지 않는 다른 일을 수행함

* DMA controller
    * 메모리에 직접 접근이 가능함 virtual memory 받아서 처리하여 잦은 interrupt를 방지하고 cpu 효율을 향상시킴

* 프로그램의 실행
    * 프로그램은 실행파일 형태로 disk에 저장되어 있음
    * 프로그램이 실행되면 binary가 memory에 올라가고 자신의 memory 공간을 할당받음
    * 실제 메모리에는 주소값이 연속적이지 않을수 있지만 각 프로그램 입장에서는 연속적으로 메모리 주소를 할당받은것 처럼 보임 이것이 virtual memory
    * 프로그램은 할당 받은 memory에 code, data, stack 영역을 나누고 사용한다.
        * code : cpu에서 실행할 기계어
        * data : code에서 사용할 전역 변수등
        * stack : 실행에 필요한 함수
    * 프로그램에서 실제로 사용할 부분만 메모리에 올리고 나머지는 disk에 대기
    * 사용이 끝난 부분은 메모리에서 제거되고 disk로 돌아감

* 커널 주소 공간의 내용
    * code : system call, interrupt 처리 코드, 자원 관리를 위한 코드, 편리한 서비스 제공을 위한 코드
    * data : cpu와 memory를 관리하기 위한 자료 구조, 프로그램마다 PCB를 생성하고 관리
    * stack : ststem call을 process당 커널 스택으로 정리

* 함수의 종류
    * 사용자 정의 함수 : 사용자가 직접 작성한 함수
    * 라이브러리 함수 : 다른 사람이 미리 만들어 둔 함수를 불러 오는것
    * 커널 함수 : system call 
