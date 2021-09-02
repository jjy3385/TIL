# 5강.운영체제 서비스

## 1.🎯프로세스 관리(Process management)

* 프로세스
  * 메모리에서 실행 중인 프로그램(program in execution)
* 주요기능
  * 프로세스 생성,소멸
  * 프로세스 활동 일시 중지, 재개
  * 프로세스간 통신(interprocess communication : IPC)
  * 프로세스 동기화(synchronization)
  * 교착상태 처리(deadlock handling)

## 2.🎯주기억장치 관리(Main memory management)

* 주요기능
  * 프로세스에게 메모리 할당
  * 메모리의 어느 부분이 프로세스에 할당되었는지 추적 및 감시
  * 프로세스 종료 시 메모리 회수
  * 효과적인 메모리 사용
  * 가상 메모리

## 3.파일 관리(file management)

* Track/Sector 로 구성된 디스크를 파일이라는 논리적 관점으로 볼 수 있도록 함
* 주요기능
  * 파일의 생성과 삭제
  * 디렉토리의 생성과 삭제
  * 기본동작지원: open,close,read,write,create,delete
  * Track/sector ~ file 간의 맵핑
  * 백업

## 4.보조기억장치 관리(Secondary storage management)

* 하드디스크, 플래시 메모리 등을 관리
* 주요기능
  * 빈 공간 관리
  * 저장공간 할당
  * 디스크 스케쥴링

## 5.입출력장치 관리(I/O device management)

* 주요기능
  * 장치 드라이브
  * 입출력 장치의 성능향상
    * buffering
    * caching
    * spooling

## 시스템 콜(System calls)

일반 애플리케이션 프로그램이 OS에게 운영체제 서비스를 받기 위해 호출(요청)하는 것

OS한테 뭔갈 부탁하는거임

