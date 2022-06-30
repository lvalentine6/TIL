cpu scheduling2 
-----------
* Multilevel Queue
  * 여러개의 ready queue를 만들어 각 queue에 우선순위를 매긴다.
    * foreground (interactive)
    * background (batch - no human interaction)
  * 각 queue는 독립적인 스케줄링 알고리즘을 가짐
    * foreground : RR 알고리즘
    * background : FCFS 알고리즘
  * 각 queue에 대한 스케줄링이 필요
    * Fixed priority scheduling
      * 우선순위가 높은 큐에 우선적으로 cpu 할당
      * 우선순위가 높은 큐에 프로세스가 없다면 다음 순위의 큐로 넘어감
      * 낮은 우선순위에 있는 프로세스는 starvation이 발생할 수 있음
    * Time slice
      * 각 큐에 cpu time을 적절한 비율로 할당
      * ex) 높은 우선순위 큐에 80%, 낮은 우선순위 큐에 20% 할당
* Multilevel Feedback Queue
  * 프로세스가 다른 큐로 이동 가능
  * 처음 들어오는 프로세스는 가장 높은 우선순위 큐로 감
  * 짧은 시간의 할당 시간을 가지고 job을 수행함
  * 할당 시간동안 job을 끝내지 못했다면 다음 우선순위 큐로 내려감
* Multiple processor scheduling
  * Homogeneous processor 경우
    * 큐에 한줄로 세워서 각 프로세서가 알아서 꺼내가게 할 수 있다.
    * 반드시 특정 프로세서에서 수행되어야 하는 프로세스가 있는 경우는 복잡해짐
  * Load sharing
    * 일부 프로세서에 job이 몰리지 않도록 부하를 적절히 공유
    * 별개의 큐를 두는 방법
    * 공동 큐를 사용하는 방법
    * ex) 화장실 칸마다 줄을 사용하는 방법
  * Symmetric Multiprocessing (SMP)
    * 각 프로세서가 알아서 스케줄링 결정
  * Asymmetric Multiprocessing
    * 하나의 프로세서가 시스템 데이터의 접근과 공유를 책임지고 나머지 프로세서는 따름
* Real time scheduling
  * Hard real time systems
    * 정해진 시간 안에 반드시 끝내도록 스케줄링 해야 함
  * Soft real time computing
    * 일반 프로세스에 비해 높은 우선순위를 갖도록 해야 함
* Thread scheduling
  * Local scheduling
    * 유저 레벨 스레드인 경우 사용자 수준의 thread library에 의해 어떤 스레드를 스케줄링 할지 결정
  * Global scheduling
    * 커널 레벨 스레드인 경우 일반 프로세스와 마찬 가지로 커널의 단기 스케줄러가 어떤 스레드를 스케줄링 할지 결정
* Algorithm Evaluation
  * Queueing models
    * 확율 분포로 주어지는 arrival rate와 service rate를 통해 performance index 값을 계산
  * Implementation & Measurement
    * 실제 시스템에서 알고리즘을 구현하여 실제 작접 성능 측정 비교
  * Simulation
    * 알고리즘을 모의 프로그램으로 작정후 trace를 입력으로 하여 결과 비교

process synchronization
-----------------
* Race condition : 데이터 읽기 -> 연산 -> 데이터 저장 하는 과정에서 같은 데이터를 공유하는 프로세서 여러개라면 데이터에 문제가 일어날수 있음
  * os에서 race condition 언제 발생하는가?
    * kernel 수행 중 인터럽트 발생 시
      * kernel 수행중에 인터럽트가 발셍하면 disable 수행이 끝나면 enable 하여 해결
    * process가 system call을 하며 kernel mode로 수행중인데 context switch가 일어나는경우
      * kernel 수행중에는 cpu를 preempt 하지 않음 kernel 모드에서 유저 모드로 돌아갈 때 preempt
    * multiprocessor에서 shared memory 내에 kernel data
      * 한번에 하나의 cpu만이 커널에 들어갈 수 있게 하는 방법
      * 커널 내부에 있는 각 공유 데이터에 접근할 때마다 그 데이터에 lock / unlock 을 하는 방법
  * Critical Section
    * n개의 프로세스가 공유 데이터를 동시에 사용하기를 원하는 경우
    * 각 프로세스에 code segment에는 공유 데이터를 접근하는 코드인 critical section이 존재
    * 하나의 프로세스가 critical section에 있을 때 다른 모든 프로세스는 critical section에 들어가면 안됨 
    * critical section : P1 -> X += 1, P2 -> X -= 1 (이러한 연산을 수행하는 부분을 말함)

   

