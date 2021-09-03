# 6강.프로세스 관리(Process Management)

* 프로세스 VS 프로그램
  * 프로세스는 실행중인 프로그램임
* 프로세스 상태
  * new , ready , running , waiting , terminated
  * 멀티프로세스 시스템까지는 running 에서 waiting 으로 가는 것만 있지만 시분할 시스템에서는 running 에서 ready 로 가는 것도 있음, 이걸 Time expired 라고 함
* Process Control Block (PCB)
  * 프로세스 제어 블록
  * 다른말로 Task Control Block (TCB)라고도 함
  * 이 블록 안에는 프로세스에 대한 모든 정보가 들어있음
  * 한개의 프로세스에 한개의 PCB가 할당됨
  * OS의 프로세스 관리 부서에 PCB 가 있는거임, 마치 정부에서 나에 대한 전산데이터를 관리하는것과 비슷함
* Queues
  * Job queue
    * Job Scheduler
      * 디스크의 프로그램을 메인메모리로 올릴 때 줄서서 기다림
    * Long-term scheduler
      * 하드디스크의 프로그램을 메모리로 올리는 처리는 몇분에 한번정도 일어남
  * ready queue
    * CPU Scheduler
      *  프로세스들이 CPU 서비스를 받으려고 줄서서 기다림
    * Short-term scheduler
      * CPU 서비스는 매우 빠른 속도로 여러 프로세스를 번갈아 처리한다
      * 그 덕에 사용자는 모든 프로세스가 동시에 수행되는것처럼 느낄 수 있음
      * 또한 여러 사용자들이 자기만 컴퓨터를 쓰고 있는 것 같은 기분이 들게 함
  * device queue
    * 프로세스가 I/O 를 쓸려고해도 줄서서 기다려야됨
* Multiprogramming
  * Degree of Multiprogramming
    * 메인메모리에 몇개의 프로세스가 올라와 있는지를 나타냄

  * i/o-bound  vs cpu-bound process
    * 특정 프로세스가 하는일이 주로 i/o 혹은 cpu 관련 작업을 한다는  뜻
    * 대표적인 i/o-bound 프로세스는 워드프로세서
    * 대표적인 cpu 프로세스는 슈퍼컴퓨터가 일기예보 예측하는거

  * Medium-term scheduler 
    * Swapping( swap out / swap in)
    * 메모리에 올라가있는 프로세스에 대해 사용자가 휴식등의 이유로 아무것도 안하는 경우가 있음
    * 그럴 때 OS는 PCB의 CPU 타임등을 끊임없이 감시하고 있다가 아무활동도 안하는 프로세스를 쫒아냄
    * 이때 하드 디스크에 프로세스 이미지를 복붙하고 메모리에서는 빼버림
      * 실제로 하드에 파일시스템의 저장공간과 프로세스 이미지를 저장하는 공간으로 나뉨
      * 이런 저장공간을 **Backing store** (swap device) 라고 함
    * 이런 처리를 swap out 이라고 함
    * 반대로 사용자가 다시 해당 프로세스를 시작하면 하드의 프로세스 이미지를 메모리로 올리는데 이 처리를 swap in 이라고 함
    * 이런 처리는 잡스케줄러처럼 너무 길지도 CPU스케줄러처럼 짧지도 않고 그 중간에 해당함

  * Context switching (문맥전환)

    > 스케줄러를 통해 프로세스가 전환되는 것을 Context switching 이라고 함

    * Scheduler 

    * Dispatcher

      * 문맥전환 시 이전 프로세스의 현재상태를 PCB 에 저장하고 실행한 프로세스의 PCB 를 복원(restore)하는 일을 하는 OS 코드

    * Context switching overhaed

      * 문맥전환 시 드는 비용

      * 문맥전환을 할 떄마다 PCB에 저장하고 다른 PCB의 값을 프로세스에 복원하는 처리를 해야하기 때문에 용량을 잡아먹는 등의 부담을 줄 수밖에 없음

        그러므로 이 코드는 로우레벨로 짜는게 좋음(어셈블리)