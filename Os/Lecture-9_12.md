Virtual Memory
--------------

* 요구 페이징
    * 프로그램 실행시 당장 사용될 페이지만을 올리는 방식
        * I/O 양 감소
        * Memory 사용량 감소
        * 빠른 응답 시간
        * 더 많은 사용자 수용
    * 유효 / 무효 비트 사용
        * 무효 비트 : 사용되지 않는 주소 영역이거나 페이지가 물리적 메모리에 없는 경우
        * 페이지의 시작에는 모든 유호 / 무효 비트가 무효로 초기화 되고 페이지가 참조되어 메모리에 올라갈때 유효로 바뀜
        * CPU가 참조하려는 페이지가 메모리에 없는 경우 페이지 부재라고 한다.
* 요구 페이징의 부재 처리
    * CPU가 참조하려는 페이지가 무효 비트라면 MMU가 trap을 발생시킴
    * 시스템이 커널모드로 전환되고 페이지 부재 처리 루틴이 호출됨
    * 해당 페이지에 대한 접근이 올바른지 확인하고 올바르지 않다면 프로세스 종료
    * 물리적 메모리에 비어 있는 프레임을 할당 받고 만약 비어 있는 프레임이 없다면 페이지중 하나를 디스크로 쫒아냄
    * 요청한 페이지를 디스크에서 메모리로 올림
    * 디스크 I/O가 끝날때까지 프로세스는 block됨
    * 메모리를 올리는 작업이 끝나면 페이지의 유효 / 무효 비트를 유효로 변경
    * 프로세스의 block을 ready로 바꾸고 ready queue로 이동
    * 프로세스가 CPU를 할당 받으면 중단 인스트럭션 부터 실행
* 요구 페이징의 성능
    * 페이지 부재의 발생 빈도가 성능에 큰 영향을 미침
    * 페이지 부재 발생 확률 (0<P<1)
        * P = 0 페이지 부재가 한번도 일어나지 않은 경우
        * P = 1 페이지 부재가 메번 발생한 경우
        * 보통 P는 0에 가깝다
    * 각종 오버헤드 : 모든 오버헤드 총합 (M)
        * 페이지 부재 발생 처리 오버헤드
        * 메모리에 빈 프레임이 없는 경우 swap out 오버헤드
        * 요창된 페이지의 swap in 오버헤드
        * 프로세스의 재시작 오버헤드
    * 유효 접근 시간 = (1-P) * 메모리 접근 시간 + P * M;
* 페이지 교체
    * 페이지 부재가 발생하여 요청된 페이지를 디스크에서 읽어오려는데 메모리에 빈 프레임이 없는 경우 메모리에 올라와 있는 페이지 중 하나를 내쫒아야 함
    * 이때 어떤 페이지를 내쫒을지 결정하는것을 페이지 교체라고 함
    * 페이지 교체 알고리즘
        * Optimal Algorithm (최적 알고리즘)
            * 가장 먼 미래에 참조될 페이지를 내쫒는 알고리즘
            * 미래에 참조될 페이지를 알아야 함으로 오프라인에서만 사용
            * 다른 알고리즘 성능에 상한선을 제공
        * FIFO Algorithm (선입 선출 알고리즘)
            * 메모리에 먼저 올라온 페이지를 먼저 내쫒는 알고리즘
            * 메모리 크기가 증가해도 페이지 부재가 늘어나는 이상현상이 발생할 수 있다.
        * LRU Algorithm (Least Recently Used)
            * 가장 오래 전에 참조가 이루어진 페이지를 쫒아내는 알고리즘
        * LFU Algorithm (Least Frequently Used)
            * 가장 적은 참조가 이루어진 페이지를 쫒아내는 알고리즘
            * 최저 참조 횟수의 페이지가 여러개 있다면 임의로 하나를 내쫒거나 가장 오래전에 참조된 페이지를 내쫒는다.
            * 자주 참조되는 페이지를 알수 있어 인기도를 반영할수 있다는 장점이 있지만 페이지의 최근성을 반영하지 못하고 구현이 복잡하다.
        * LRU와 LFU 비교
            * LRU는 정렬된 LinkedList 방식으로 페이지를 교체할 때 가장 위에 있는 LRU 페이지를 교체하면 되고, 특정 페이지가 참조되었을 때는 List의 맨 아래로 바로 보내면 되므로 구현이
              간단하고 시간 복잡도가 O(1)이다.
            * LFU는 페이지를 교체할 때는 가장 위에 있는 LFU 페이지를 교체하면 되지만, 특정 페이지가 참조되었을 때는 자기 자신보다 아래에 있는 노드와 참조 횟수를 모두 비교해야 하므로 일반적인
              List를 사용하면 시간 복잡도가 O(N)이 된다. 그래서 인접 노드 간의 참조 횟수를 빠르게 비교하기 위하여 Heap 자료 구조를 사용하며, 이것의 시간 복잡도는 O(log N)이 된다.
