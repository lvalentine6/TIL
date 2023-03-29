cpu scheduling
--------------
* scheduling criteria (성능 척도)
  * cpu 입장에서의 성능척도
    * cpu utilization(이용률)
      * 전체 처리 시간에서의 cpu를 사용한 시간의 비율 측정
    * Throughput(처리량)
      * 주어진 시간동안 몇개의 작업을 많이 했는지 측정
  * 프로세스 입장에서의 성능척도
    * Turnaround time(소요시간, 반환시간)
      * waiting time, Response time을 포함한 전체 시간
    * Waiting time(대기시간)
      * ready queue에서 cpu를 사용하기 위해 대기한 시간
    * Response time(응답 시간)
      * 최초로 cpu를 사용하기까지 기다린 시간
* cpu scheduling algorithm
  * FCFS(first come first served)
    * 프로세스의 도착 순서에 따라 대기시간이 다름
  * SJF(shortest job first)
    * 각 프로세스의 다음번 cpu burst time을 가지고 스케줄링에 활용
    * cpu burst time이 가장 짧은 프로세스를 제일 먼저 스케줄
      * Nonpreemptive
        * 일단 cpu를 잡으면 cpu burst가 완료될 때까지 cpu를 뺏기지(preemptive) 않음
      * Preemptive
        * 현재 수행중인 프로세스의 남은 burst time보다 더 짧은 cpu burst time을 가지는 프로세스가 도착하면 뺏김
        * SRTF(Shortest remaining time first) 라고도 부름
    * SJF는 주어진 프로세스에 대해 minimum average waiting time을 보장
    * 문제점 1 : Burst time이 긴 프로세스는 cpu를 영원히 사용하지 못할수도 있다.(starvation) 
    -> aging을 통해 해결 : 기다린 시간만큼 우선순위를 올림
    * 문제점 2 : cpu 사용시간을 미리 알 수 없다.
  * cpu burst time 예측
    * 다음번 cpu burst time은 과거의 cpu burst time을 이용해서 추정 (Exponential Averaging)
  * Priority scheduling
    * 높은 우선순위(정수로 우선순위를 표현)를 가진 프로세스에게 cpu 할당
  * Round Robin(RR)
    * 각 프로세스는 동일한 크기의 할당시간을 가짐
    * 할당 시간이 지나면 프로세스는 preempted 당하고 ready queue 제일 뒤에 가서 줄을 선다
    * n개의 프로세스가 ready queue에 있고 할당시간이 q time unit인 경우 프로세스는 최대 q time unit 단위로 cpu를 1/n 얻음
    * 어떤 프로세스도 (n-1)q time unit만큼 기다리지 않음
    * Response time이 빠르다는 장점
    * q가 크면 -> FCFS
    * q가 너무 작으면 문맥교환으로 오버헤드가 커짐
    * 모든 프로세스의 burst time이 같다면 Turnaround time이 늘어날수도 있음
