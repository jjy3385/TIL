# 7~9.CPU Scheduling(스케줄링)

> 💡Ready Q 안에 혹은 메인메모리에 여러개의 프로세스가 줄서서 기다리고 있을 때 현재 진행중인 프로세스가 끝나면 그 중에 어떤 프로세스를 선택해서 CPU의 서비스를 받게 할 것인지를 결정하는 것

## Preemptive VS Non-Preemptive

* Preemptive(선점)

  * 응급환자가 들어온 경우와 같음
  * CPU가 진행중인 프로세스를 중단하고 다른 프로세스를 진행하는 경우

* Non-preemptive (비선점)

  * 현재 진행중인 프로세스가 끝날때까진 스케줄링을 하지 않는 방식

* Scheduling criteria (스케줄링 척도/기준)

  * CPU Utilization (CPU 이용률)
  * Throughput (처리율) 
  * Turnaround time (반환시간) 
    * 병원문을 들어서는 순간부터 나서는 순간까지
    * 의사샘 진료받으려고 기다렸다가 진료끝나면 X-ray 찍으려고 그 앞에 잠시 기다렸다가 X-ray 다 찍었으면 다시 진료실 앞에서 기다렸다가 또 진료받음, 그런 모든 과정이 끝나야 집에 갈 수 있음
    * 프로세스 스케줄링은 이와 매우 유사해서 CPU 서비스받으려고 Ready Q 에서 기다리다가 CPU가 프로세스를 돌리게 되고 그러다가 I/O 를 쓰기 위해 또 기다리고 그게 끝나면 다시 Ready Q 에 들어오는 그러한 과정을 반복하다가 프로세스가 메모리에서 완전히 내려가면 끝나는 것임
  * Waiting time(대기시간)
  * Response time(응답시간)

  # CPU Scheduling Algorithms

  >  💡CPU 는 작업을 처리하고 있고 Ready Q에서 프로세스들이 줄서서 기다리고 있는데 지금 하는 작업이 끝나면 다음엔 어떤 프로세스가 들어갈 것인가? 이걸 결정하는게 CPU스케줄링 알고리즘이다

  ## First-Come, First-Served(FCFS)

  * 단순하고 공평하지만 꼭 좋은 성능을 보장하지는 않음
  * Gantt chart
  * Convoy  Effect(호위효과)
    * CPU 시간을 많이 쓰는 녀석이 앞에 있으면 나머지는 뒤에서 기다려야됨(따라가야됨)
    * 화장실을 3명이 갔는데 큰일보는친구가 먼저 들어가면 나머지 2명은 하염없이 기다려야됨
    * 물론 이 경우엔 스케줄링 척도를 WT(waiting time)만 비교한거임
  * Non-Preemptive Scheduling 임
    * 먼저 들어간 작업이 끝날떄까지 기다리니까

  ## Shortest  - Job - First (SJF)

  * 대기시간을 줄이는 측면에서 증명된 가장 좋은 방법임
  * 하지만 현실적이지 못함
    * 어떤 프로세스가 CPU 시간을 얼마나 사용할지는  정확히 알수가 없음
    * 물론 통계적으로 예측이 가능하지만 이것도 오버헤드가 발생하기 떄문에 이 방법은 좀 어려움
  * Preemptive or Non-Preemptive 둘다 가능
    * Preemptive 는 Shortest-Remaining-Time First 라고 할 수 있음
    * 즉, 최소잔여시간 우선하여 진행함
    * 평균 대기시간 계산하는 문제가 잘 나올 수 있음... 아마 정보처리기사에 나오지 않을까?

  ## Priority Scheduling

  * 낮은값이  우선순위가 높음
  * 우선순위를 결정하는 요소
    * 내부적인 요소 :  Time limit, memory requirement, i/o to CPU burst...
    * 외부적인 요소 : amount of funds being paid, political factors .... (돈낸만큼,정치적인 요소 등등)
  * Preemptive or Non-Preemptive 둘다 가능
  * 문제점
    * Indefinite blocking : starvation (기아)
      * 너무 우선순위가 낮은 작업의 경우 CPU 서비스를 오랫동안 기다려도 못받을 수 있음
    * 해결방법 : aging
      * OS 가 주기적으로 Ready Q 를 검사해서 어떤 프로세스가 Ready Q 에 오래 머물러 있다면 점진적으로 우선순위를 높여주는 방식

  ## Round-Robin

  >  💡영어가 삥삥도는 새를 뜻함

  *  Time-Sharing System (시분할/시공유 시스템)과 연관있음

    * 작업중인 프로세스를 정해진 시간만큼만 돌리고 계속 전환해주는 방식임

  * Time quantum (시간양자) 를 얼마로 정하는지가 성능에 가장 큰 요인임

  * Preemptive scheduing 

    > ❓ 왜지?

  * Performance depends on the size of the time quantum

  ## Multilevel Queue Scheduling (멀리레벨 큐 스케줄링)

  > 🎯프로세스 그룹에 따라 큐를 여러개 두고 각각의 큐에 그룹에 알맞는 스케줄링 알고리즘을 적용하는 방식

  * Process groups
    * System process
      * OS 관련 처리, 가장 긴급하고 중요함
    * Interactive processes 
      * 대표적으로 게임이 있음
    * Inteactive editing processes
      * 워드 프로세스
    * Batch processes
      * 일괄처리, 대표적으로 컴파일, 컴퓨러와 대화가 필요없음
      * 인터렉티브 프로세스보다는 느려도 큰 문제가 없음
    * Student processes 


## Multilevel Feedback Queue Scheduling

* 복수개의 Queue
* 다른 Queue 로의 점진적 이동이 가능하도록 피드백을 함
  * 모든 프로세스는 하나의 큐를 통해 진입하게 되는데 피드백을 통해 그 통로를 바꿔주는 것임
  * 너무 많은 CPU time 사용 시 다른 Quere 로 이동
  * 기아 상태 우려시 우선순위가 높은 Quere 로 이동

# Process Ceration (프로세스 생성)

* 프로세스는 프로세스에 의해 만들어진다! 
* 그러므로 부모,자식,형제 프로세스가 있음
  * Parent process
  * Child process
  * Sibling process
* 계층관계를 프로세스 트리라고 함
* Process ID (PID)
  *  보통 Interger 값으로 0부터 순서대로 채번되며 유니크함
* 프로세스 생성 
  * 프로세스 생성 시스템 콜: fnk() 
    * 메모리에 프로세스 생성(현재 프로세스에는 아무것도 없음)
  * 프로세스 실행 시스템 콜: exec()
    * 빈 프로세스에 프로그램을 복사