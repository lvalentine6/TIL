Deadlock
---------------

* Deadlock : 프로세스들이 서로가 가진 자원을 기다리며 block된 상태
  * Resource : 하드웨어, 소프트웨어 등을 포함하는 개념
    * IO 디바이스, cpu cycle, memory space, semaphore...
  * 데드락 발생 조건
    * Mutual exclusion(상호배제)
      * 매 순간 하나의 프로세스만이 자원을 사용할 수 있음
    * No preemption(비선점)
      * 프로세스는 자원을 스스로 내어놓을뿐 강제로 빼앗기지 않음
    * Hold and wait(보유대기)
      * 자원을 가진 프로세스가 다른 자원을 기다릴 때 보유 자원을 놓지않고 계속 가지고 있음
    * Circular wait(순환대기)
      * 자원을 기다리는 프로세스간에 사이클이 형성되어야 함
  