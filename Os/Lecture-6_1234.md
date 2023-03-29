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
* Synchronization Problem solve
    * Bounded Buffer Problem
        * 생산자 - 소비자 문제
        * 생산자는 empty 버퍼가 있는지 확인하고 없다면 기다린다,
        * 공유데이터에 락을 걸고 버퍼 조작
        * 끝나면 락을 풀고 full 버퍼 증가
        * 소비자는 full 버퍼가 있는지 확인하고 없다면 기다린다.
        * 공유데이터에 락을 걸고 버퍼 조작
        * 락을 풀고 empty 버퍼 증가
        * 생산자 여러명이 동시에 한 버퍼에 데이터를 쓰거나 소비자 여러명이 동시에 한 버퍼에서 데이터를 읽어갈 수 있는 문제가 있음
        * 공유테이터 새마포어와 남은 버퍼의 개수를 표시하는 세마포어 두개의 세마포어를 사용하여 문제를 해결한다.
    * Readers Writers Problem
        * 한 프로세스가 DB에 접근하여 데이터 쓰기 작업중일때 다른 프로세스가 접근하면 안됨
        * 데이터 읽기 작업은 여러 프로세스가 진행 가능
        * Reader와 Writer의 접근을 판단하는 db 세마포어와 리드카운트를 보장하기 위한 세마포어 사용
        * Writer가 작업을 하고 싶어도 계속 Reader가 온다면 starvation에 빠질수 있다
        * -> Writer가 대기하고 있다면 일정 시간이 지나고 Writer의 작업을 보장하여 starvation 방지
    * Dining Philosophers Problem
        * 다섯명의 철학자가 원형 식탁에서 생각하거나 음식을 먹는다.
        * 철학자 각자의 왼쪽과 오른쪽에 젓가락이 하나씩 있다.
        * 음식을 먹으려 할때는 왼쪽 젓가락 부터 든다. 만약 젓가락이 없다면 기다린다.
        * 왼쪽 젓가락을 들었다면 오른쪽 젓가락을 든다. 만약 젓가락이 없다면 기다린다.
        * 양쪽 젓가락을 다 들었다면 음식을 먹는다.
        * 음식을 다 먹었다면 오른쪽 젓가락을 내려놓고 왼쪾 젓가락을 내려놓는다.
        * 만약 동시에 다섯명의 철학자가 음식을 먹으려 왼쪽 젓가락을 든다면 모두가 오른쪽 젓가락을 기다리는 데드락에 빠진다.
        * 해결방안
            * 4명의 철학자만 동시에 테이블에 앉을수 있게 한다.
            * 젓가락을 두개 집을수 있을 때만 젓가락을 집을 수 있게 한다.
            * 짝수 철학자는 왼쪽 젓가락부터 잡도록 방향을 비대칭으로 정한다.
    * 세마포어의 문제점
        * 코딩하기 힘들다.
        * 정확성의 입증이 어렵다 -> 디버그 하기 어렵다.
        * 자발적 협력이 필요하다.
        * 하나의 실수가 모든 시스템에 치명적인 영향을 끼친다.
* Monitor
    * 동기화 문제를 해결할 수 있는 고수준 도구
    * 프로세스가 공유 데이터에 접근하기 위해서는 모니터 내부의 프로시저를 통해서만 공유 데이터에 접글할 수 있게 함
    * 프로그래머가 락을 걸 필요가 없어 간단하다.
    * 위의 세가지 문제 모두 모니터로 해결 가능
