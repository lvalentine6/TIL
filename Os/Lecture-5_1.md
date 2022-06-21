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