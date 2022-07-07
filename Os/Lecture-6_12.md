process synchronization2
------------------
* Critical Section 
  * 소프트웨어적 해결볍의 충족 요건
    * Mutual Exclusion
      * 하나의 프로세스가 Critical Section 부분을 수행중이면 다른 프로세스의 접근 차단
    * Progress
      * Critical Section에 어떤 프로세스도 없고 Critical Section을 수행하기 원하는 프로세스가 있다면 허가
    * Bounded waiting
      * Critical Section에 들어가는 횟수 제한 (starvation 방지)
  * 해결 알고리즘
    * 1: while문을 이용하여 자신의 turn이 아닐경우 기다리다 Critical Section 수행
    -> Critical Section에 들어가고 싶은지 알 수 없어 progress 위반
    * 2: 각 프로세스들이 boolean flag 값을 가지고 있어 Critical Section에 들어가고 싶은지 표시
    -> 서로 끊임없이 양보하는 상황이 발생할 가능성이 있음
    * 3(Peterson's algorithm) : 1 + 2 알고리즘 모두 사용
    -> 모든 해결법을 충족하지만 계속 cpu와 memory를 사용하면서 Busy waiting이 발생할 수 있다.
  * 하드웨어적 해결 방법
    * read와 write를 동시에 진행하면 간단하게 해결 가능 (Test and set)
  * Semaphores
    * 앞의 방식들을 추상화 시켜 프로그래머가 간단하게 사용할 수 있게 함
    * Semaphores S = 정수값읠 가짐
    * P연산 : 변수값을 획득, 공유데이터 획득
    * V연산 : 사용이 끝나고 반납
    * Block / wakeup implementation
      * 공유데이터를 다른 프로세스가 사용하고 있다면 block 시키고 자신의 차례가 오면 wakeup 시킴
    * Busy-wait vs Block/wakeup
      * 일반적으로는 Block/wakeup 더 좋다.
      * Critical Section이 짧다면 Block/wakeup의 오버헤드가 더 클수 있기 때문에 Busy-wait가 적당함
      * Critical Section이 길다면 Block/wakeup이 적당함
    * Deadlock / Starvation
      * Deadlock : 둘 이상의 프로세스가 서로 상대방에 의해 충족될 수 있는 이벤트를 무한히 기다리는 현상
      * Starvation : 프로세스가 suspend된 이유에 해당하는 세마포어 큐에서 빠져나갈 수 없는 현상