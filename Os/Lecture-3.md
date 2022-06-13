프로세스
------------
* 프로세스 : 실행중인 프로그램
  * 프로세스의 문맥 
    * cpu 수행 상태를 나타내는 하드웨어 문맥
      * 프로그램 카운터
      * 각종 레지스터
    * 각종 프로세스의 주소 공간
      * code, data, stack
    * 프로세스 관련 커널 자료 구조
      * PCB(process Control Block)
      * Kernel stack
  * 프로세스의 상태
    * running
      * cpu를 점유하고 instruction을 수행중인 상태
    * ready
      * cpu를 기다리는 상태(메모리등 다른 조건을 모두 만족하고)
    * blocked(wait, sleep)
      * cpu를 주어도 당장 instruction을 수행할 수 없는 상태
      * 프로세스 자신이 event(IO등) 즉시 만족되지 않아 이를 기다리는 상태
    * suspended(stopped)
      * 외부적인 이유로 프로새스의 수행이 정지된 상태
      * 프로세스는 통째로 디스크에 swap out됨
      * 사용자가 프로그램을 일시 정지시킨 경우, 시스템이 여러 이유로 프로세스를 일지 정지시킴(swapper)
    * new : 프로세스가 생성중인 상태
    * terminated 수행이 끝난 상태
    * blocked : 자신이 요청한 event가 만족되면 ready
    * suspended : 외부에서 resume해 주어야 active
  * 프로세스의 상태
    * new -> ready(in memory) -> running -> waiting -> terminated
    * cpu <-> ready queue <-> IO queue <-> resource queue
      * 프로세스들이 os의 제어에 따라 각 running과 queue를 순회함
      * 커널은 각 프로세스마다 PCB를 생성하여 관리
      * 프로세스가 본인의 코드를 실행중인 상태 : user mode running
      * 프로세스가 system call, interrupt, trap 하게 되어 실행중인 상태 : kernel mode running
  * PCB(process control block) : os가 각 프로세스를 관리하기 위해 프로세스당 유지하는 정보
    * os가 관리상 사용하는 정보
      * process state, process id, scheduling information...
    * cpu 수행 관련 하드웨어 값
      * program counter, registers
    * 메모리 관련
      * code, data, stack
    * 파일관련
      * open file description...
  * 문맥 교환(context switch) : cpu를 한 프로세스에서 다른 프로세르로 넘겨주는 과정
    * cpu를 내어주는 프로세스의 상태를 그 프로세스의 pcb(data 부분)에 저장
    * cpu를 새롭게 얻는 프로세스의 상태를 pcb에서 읽어옴
    * system call이나 interrupt 발생시 반드시 문맥교환이 일어나는건 아님
    * 1. user mode(프로세스 A) -> kernel mode -> user mode(프로세스 A) : 문맥교환 아님
    * 2. user mode(프로세스 A) -> kernel mode -> user mode(프로세스 B) : 문맥교환 일어남
    * 1번의 경우에도 문맥이 save되지만 문맥교환이 더 큰 부담을 줌(캐시메모리 삭제)
  * 프로세스를 스케줄링하기 위한 큐
    * job queue
      * 현재 시스템 내에 있는 모든 프로세스의 집합
    * ready queue
      * 현재 메모리 내에 있으면서 cpu를 점유하여 실행되기를 기다리는 프로세스의 집합
    * device queue
      * IO device의 처리를 기다리는 프로세스의 집합
  * 스케줄러(scheduler)
    * long-term-scheduler(장기 스케줄러 or job scheduler)
      * 시작 프로세스 중 어떤 것들을 ready queue로 보낼지 결정
      * 프로세스에 memory등 각종 자원을 주는 문제
      * degree of multiprogramming(메모리에 올라가는 프로세스의 수)을 제어
      * 메모리에 너무 적은 프로세스가 올라가면 cpu낭비 너무 많은 프로세스가 올라가면 성능 저하
      * timesharing system에는 보통 장기 스케줄러가 없음(무조건 ready)
    * short-term-scheduler(단기 스케줄러 or cpu scheduler)
      * 어떤 프로세스를 다음번에 running 시킬지 결정
      * 프로세스에 cpu를 주는 문제
      * millisecond 단위로 빨라야 함
    * medium-term-scheduler(중기 스케줄러 or swapper)
      * 여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫒아냄
      * 프로세스에게서 memory를 뺏는 문제
      * deree of multiprogramming을 제어