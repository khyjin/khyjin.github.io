---
title:  "[정리]5장 컴퓨터 아키텍처와 운영체제"
excerpt: "한권으로 읽는 컴퓨터 프로그래밍"

categories:
  - book-review
tags:
  - [book, review]

toc: true
toc_sticky: true

date: 2022-01-21
last_modified_at: 2022-01-21
layout: single
---

[출처 - 한권으로 읽는 컴퓨터 프로그래밍](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=268444562)

---------------------------------------

아키텍처 : 컴퓨터의 여러 구성요소를 배치하는 방법

### 기본적인 구조 요소들
* 컴퓨터 구조 - 폰노이만, 하버드 구조(차이점은 메모리 뿐)
    * 폰 노이만 : 메모리에서 동시에 명령어와 데이터를 가져올 수 없다
    * 하버드 : 동시에 명령어와 데이터를 가져올 수 있어서 좀더 빠르지만 두번째 메모리를 처리하기 위한 버스가 더필요하다. 명령어가 별도의 메모리에 존재.
* 프로세스 코어 : 예전의 CPU
* 마이크로 프로세서와 마이크로 컴퓨터
    * 마이크로 프로세서 : 메모리와 I/O가 프로세서 코어와 같은 패키지에 들어있지 않은 프로세서. 보통 큰 시스템에 들어가는 부품.
    * 마이크로 컴퓨터 : 모든 요소를 한 칩안에 패키징한 것. 단일 칩으로된 작은 컴퓨터.

### 프로시저, 서브루틴, 함수
* 함수(프로시저나 서브루틴 -> 프로그래밍 언어에 따라 이름이 다를 뿐 동일한 것) 코드를 재사용하는 주요수단.
* 함수 호출 흐름
    * 반환주소 저장 -> 함수 파라미터 -> 함수로 분기 -> 함수 바노한뒤 계속 실행

### 스택
* 재귀함수 : 함수가 자기자신을 호출하는 경우
* 재귀함수가 제대로 작동하기 위해서는 반환주소를 여럿 저장하고, 함수에서 호출지점으로 반환 할 때 저장된 주소 중 어떤 구조를 사용할 지 결정할 수 있어야 한다. 이 때 사용되는 구조가 스택(Last In First Out, LIFO 구조)

### 인터럽트
* 실행 중인 프로그램을 잠깐 중단 시켜서 주의를 기울여야 하는 외부의 요소에 대응할 수 있게 만들 방법 필요 
* 인터럽트 시스템 : 적절한 신호가 들어오면 CPU 실행을 잠깐 중단시킬수 있는 핀 혹은 전기 연결
* 주변 장치가 인터럽트 요청 생성 -> 현재 실행중인 명령어 실행 후 실행 중인 프로그램을 중단. 인터럽트 핸들러 실행 -> 다시 원래의 프로그램 중단 위치부터 실행

### 상대 주소 지정
* 운영체제 커널 : 여러 프로그램을 동시에 실행 할 떄 각 프로그램을 서로 전환시켜주는 일종의 관리자 프로그램
* 상대 주소 지정 : 명령어에 들어 있는 주소를 0부터 시작하는 위치로 해석하지 않고, 명령어의 주소를 기준으로 하는 상대적 주소로 해석
* 상대 주소지정을 사용하면 프로그램을 메모리의 원하는 위치로 재배치 할 수 있다.

### 메모리 관리 장치
* 메모리 관리 장치(MMU)는 대부분 마이크로 프로세서에 있는 복잡한 하드웨어
* MMU는 가상주소를 물리주소로 변환

### 시스템 공간과 사용자 공간
* CPU에는 시스템 모드인지 사용자 모드인지 결정하는 비트가 들어있다.
* I/O를 처리하는 명령어는 시스템 모드에서만 실행가능. 사용자 모드에서 실행중인 프로그램이 시스템 모드 프로그램에게 요청을 보낼 수 있다.
* 위의 방식의 장점으로 
    1. 사용자 프로그램으로부터 운영체제 보호
    2. 운영체제가 프로그램에 대한 자원할당을 전적으로 제어 가능

### 메모리상의 데이터 배치
* 프로그램을 작성할 때 메모리가 얼라마 필요한지 알고있는 경우는 '정적(static)데이터', 프로그램을 실행하기 전에는 크기를 알 수 없는 데이터를 '동적(dynamic)데이터' 라고 한다.
* 동적 데이터는 정적데이터가 차지하는 영역의 바로 위에 쌓이며 이를 힙(heap)이라 한다.

