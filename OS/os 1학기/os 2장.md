## System call

**System Call(시스템 호출)** 은 응용 프로그램(Application Program)이 운영체제(OS)에게 특정 서비스를 요청하는 메커니즘이다 

Typically the library as an intermediary -> 라이브러리(Library)가 중간에서 인터페이스 역할을 함

**컴파일: 소스 코드(ex: C, C++, Python 등으로 작성된 코드)를 기계어 코드로 변환하는 과정**

컴퓨터가 이해할 수 있도록 프로그래밍 언어로 작성된 코드를 이진 파일로 변환함

**디버깅: 프로그램이 예상대로 동작하지 않거나 오류가 발생하는 부분을 찾아 수정하는 과정**

<br/>

## Important design principle

정책(Policy): **무엇을 할 것인가**를 결정

메커니즘(Mechanism): **어떻게 실행할 것인가**를 구현

<br/>

<예시 1>

정책(Policy): 응용 프로그램이 운영체제에게 서비스를 요청할 수 있도록 허용

메커니즘(Mechanism): **시스템 호출(System Call)** 을 제공하여 요청을 처리

<br/>

<예시 2>

정책(Policy): CPU 자원을 어떻게 관리할 것인지 결정

메커니즘(Mechanism): 타이머(Timer)를 이용하여 CPU 점유 시간을 관리

<br/>

## POSIX (Portable Operating System Interface)

POSIX : 유닉스 기반 운영체제 간의 표준화된 인터페이스를 정의하는 규격 (윈도우는 지원 x )

POSIX를 사용하면 **운영체제 간 이식성(Portability)을 보장할 수 있음** -> 리눅스, macOS, BSD, AIX 등 다양한 운영체제에서 POSIX API를 사용하면 **코드 수정 없이 실행 가능**

운영체제마다 시스템 호출이 다르므로, API를 사용하면 운영체제에 맞게 **내부적으로 시스템 호출을 처리할 수 있다**

<br/>

예를 들어 우리가 코드를 작성할 때 print()라고 쓰면 우리가 작성한 print() 코드는 직접 운영체제 시스템 호출을 하지 않음

**대신, 표준 라이브러리가 운영체제에 맞게 적절한 API를 호출하여 실행되도록 처리함.**

이때 라이브러리란 미리 구현된 코드들의 집합이다 

예를 들어, Python의 print()는 실제로 **sys.stdout.write()** 라는 함수(라이브러리 함수)를 호출해서 출력 작업을 처리한다
 
<br/>

**정리하면 우리가 사용하는 코드를 OS마다 문법에 맞게 변환해주는게 POSIX임**

<br/>

## System call interface

시스템 호출 인터페이스는 System Call과 운영 체제를 연결하는 역할을 수행함

1. 각 시스템 호출에는 특정 번호(Number)가 할당되어 있음

2. 해당 번호를 기준으로 색인화된(Indexed) 테이블(Table)이 존재함

3. 운영 체제(OS) 커널에서 의도된 시스템 호출을 실행하고, 시스템 호출의 상태 및 반환 값을 반환함

ex) sys_exit(), sys_fork()

**즉, 고유 번호로 할당된 테이블을 이용해서 쉽고 간단하게 호출하기 위해 사용**

![image](https://github.com/user-attachments/assets/c38beaec-7f44-4468-bdbf-398ef919a43f)

<br/>

## register


시스템 호출에서 매개변수 전달하는 방식

1. 가장 간단한 방식: 매개변수를 register에 직접 저장하여 전달함. 하지만, 레지스터 개수는 제한적이므로(ex: 리눅스는 register을 최대 6개까지 받을 수 있음), 매개변수가 많아질 경우 사용하기 어려움

2. 추가적인 경우: 매개변수의 개수가 레지스터보다 많을 수 있음 이때, 매개변수를 메모리의 블록(block) 또는 테이블(table) 에 저장한 후, 해당 블록의 주소(address)를 레지스터를 통해 전달함

<br/>

## 레지스터에 저장하는 것이 효율적인 이유

**레지스터는 메모리보다 훨씬 빠름**

CPU는 레지스터에서 데이터를 즉시 읽고 쓸 수 있음

반면, 메모리는 메모리 접근 시간이 존재하므로, 데이터를 읽고 쓰는 데 추가적인 시간이 필요하다

**레지스터는 CPU 내부에 존재하기 때문에**, 캐시보다도 빠른 속도로 데이터를 처리할 수 있음 (캐시는 CPU와 메모리 사이에 존재)

즉, 거리가 CPU(register 내부 존재) - Cache - memory 이렇게 되어 있어서 효율적인 순서도 register, Cache, Memory임 

<br/>

## 구조 설명

![image](https://github.com/user-attachments/assets/29f6c55c-46a3-45a2-88ea-c6038ff54528)

<br/>

```ruby
 fork()
 {
     ….
     movl 2, %eax
     int $0x80
     ….
 }
 ….
```

위 코드에서 movl 2, %eax는  **2라는 값을 %eax 레지스터에 저장한다는 의미**

int $Ox80(16진수 128) 에서 **int는 인터럽트를 유발한다는 의미 (정수형이 아님)** 이고 128번에 인터럽트 번호를 갖는 인터럽트를 유발한다는 뜻

예시 설명 

1. user task에서 fork() 함수 실행

2. libc.a 에서(C Standard Library : C 언어로 작성된 프로그램이 사용하는 정적 라이브러리 파일) fork()와 같은 system call을 사용할 때, 해당 라이브러리가 system call을 호출할 수 있도록 연결함, **즉 user space 에서 system call을 사용하기 위한 인터페이스임**. 

3. IDT(리눅스에서 interrupt vector 의미)에서 Ox80(=128 16진수) 번을 실행 -> IDT에서 128번이 systemm call을 의미함 

4. system call을 호출하면 kernel에서 먼저 기존 코드로 돌아가기 위해 **SAVE_ALL**로 user에서 넘어가기 전 부분을 기록함. 그리고 sys_call_table을 실행 -> 여기서 4는 sys_call_table에서 함수 주소를 찾을 때 필요한 크기이다 (sys_call_table에서 함수 포인터가 4바이트 간격으로 저장되기 때문)

5. sys_call_table에서 2번(sys_fork())을 실행하여 fork()함수를 실행할 수 있게 되는 것임

<br/>

## System program 

대부분의 사용자는 시스템 호출(sys_read(), sys_write() 등)을 직접 호출하지 않음 대신, 시스템 프로그램을 통해 운영 체제와 상호작용함

운영 체제의 설계와 구현은 단순한 문제 하나를 해결하는 방식이 아니라 다양한 접근법이 필요함

1. 사용자 목표 (User Goals) :	사용자 입장에서 운영 체제가 편리하고 신뢰할 수 있도록 설계하는 것

2. 시스템 목표 (System Goals) : 	운영 체제가 개발 및 유지보수하기 쉽고, 안정적이고 효율적으로 동작하도록 설계하는 것

<br/>

## Layered approach 

The bottom layer (layer 0), is the hardware

The highest (layer N) is the user interface

각 레이어는 시스템의 나머지 부분에 대한 걱정 없이 디버깅할 수 있다는 것이 장점 -> 디버깅과 구조가 단순 (디버깅 : 프로그램을 실행했을 때 예상과 다른 동작(버그)이 발생하는 경우, 그 원인을 분석하고 수정하는 과정)

**각 계층이 엄격하게 분리되어 있어서 자체적으로 디버깅이 가능**

<br/>

## MicroKernel

정의 : 마이크로커널 아키텍처는 운영 체제의 **핵심 기능을 가능한 한 작고 효율적인 커널로 유지하는 것**

process 간의 communication이 많음

kernel이 처리하는 요소 process, I/O device, storage, memory 에서 **process와 memory만 가지고 있음**, 나머지는 user mode

<br/>

**장점**

1. Easier to extend a microkernel : 커널 자체가 최소화되어 있기 때문에 새로운 기능을 추가하거나 기존 기능을 확장하는 것이 상대적으로 쉬워짐

2. Easier to port the operating system to new architectures : 새로운 하드웨어 아키텍처에 맞추어 포팅하는 과정이 상대적으로 수월(최소화되어 있기 때문, 여기서 port란 소프트웨어가 다른 하드웨어나 소프트웨어 환경으로 이전되는 과정)

3. More reliable (less code is running in kernel mode) : 커널 모드에서 실행되는 코드가 적기 때문에 시스템 안정성 및 신뢰성 향상

<br/>

**단점**

**message passing overhead 발생 가능성이 높음**

<br/>

## Modules

module :  운영체제 커널의 독립적인 코드 조각으로, 커널 기능을 확장하거나 특정 하드웨어를 지원하기 위해 동적으로 로드(삽입)하거나 언로드(제거)할 수 있는 재사용 가능한 단위

**<예시>**

1. 하드웨어 드라이버 : 특정 하드웨어 장치(예: USB, GPU, 네트워크 카드 등)를 제어하고 커널과 통신할 수 있도록 하는 코드

2. 파일 시스템 : 운영체제에서 특정 파일 시스템(예: FAT32, NTFS, ext4 등)을 지원하도록 하는 모듈

3. 네트워크 프로토콜 모듈 : 네트워크 통신에 사용되는 특정 프로토콜(예: TCP/IP, UDP, Netfilter 등)을 구현하는 모듈
 
<br/>

## Module 특징

1. **독립성** : 모듈은 커널 내에서 독립적으로 동작하며, 특정 기능이나 하드웨어에만 집중하도록 설계됨 (예: USB 드라이버 모듈, 네트워크 프로토콜 모듈)

2. **동적 관리 가능** : 커널의 실행 중에도 insmod 명령으로 모듈을 추가하거나 rmmod 명령으로 제거 가능. 운영체제를 재부팅하지 않고 기능 추가 및 제거를 지원.

3. **효율성** : 필요할 때만 로드하여 메모리를 효율적으로 사용하며, 불필요한 자원을 소비하지 않음.

4. **확장성** : 새로운 기능이나 드라이버를 쉽게 추가할 수 있어, 운영체제의 유지보수성과 확장성을 크게 높임.

5. **커널과의 통합** : 모듈은 커널과 통합되어 작동하지만, 커널의 핵심 부분을 수정하지 않아도 새로운 기능을 추가할 수 있음.

<br/>

## Dynamic Module linking

의미 : **커널에 모듈을 동적으로 추가하거나 제거할 수 있는 기능으로, 이를 통해 컴퓨터를 재부팅하지 않고도 새 모듈을 로드하거나 기존 모듈을 언로드할 수 있음**

Linux는 dynamic loading과 unloading을 지원함

insmod : 커널에 모듈을 삽입하는 명령어

rmmod : 커널에서 모듈을 제거하는 명령어

<br/>

## Virtual machine 

Virtual machine : 컴퓨터 하드웨어를 소프트웨어로 추상화하여, 하나의 물리적 머신에서 여러 개의 독립적인 컴퓨팅 환경을 제공하는 기술

각 프로세스에는 기본 컴퓨터의 **가상 사본(virtual copy)** 이 제공됨

가상 사본을 제공한다는 것은 **실제 하드웨어의 자원을 빌려서, 가상 환경에 맞게 가상 하드웨어를 제공한다는 의미이다**

<예시>

**1. CPU 자원 복사**

가상화 소프트웨어는 실제 물리적 CPU의 일부 자원을 할당하여 가상 CPU를 만듦

실제 CPU 자원을 부분적으로 복사한 것임. 게스트 OS는 이 가상 CPU를 자신의 실제 CPU처럼 사용한다

<br/>

**2. 메모리 자원 복사**

물리적 RAM의 일부를 가상 메모리로 할당하여, 게스트 OS가 이를 자신의 RAM처럼 사용하게 만듦

물리적 RAM의 일부를 복사본처럼 제공하는 것임

<br/>

**3. 디스크 자원 복사**

물리적 디스크의 일부 공간을 가상 디스크로 할당하여, 게스트 OS가 이를 자신의 디스크처럼 사용함

실제 하드디스크의 일부 공간을 가상 환경에서 복사본처럼 사용하는 것임

<br/>


비유: 빌려주는 방 (공유 오피스)

물리적 컴퓨터(진짜 하드웨어)는 큰 건물

가상 머신은 이 건물 안에 있는 작은 방처럼 생각하면 됨

각 방(가상 머신)은 자기만의 책상, 컴퓨터, 인터넷(하드웨어 자원)을 가진 것처럼 보이지만, 사실은 건물(물리적 컴퓨터) 전체를 여러 방이 나눠 쓰고 있는 것과 동일 

<br/>

![image](https://github.com/user-attachments/assets/90fcf260-f76c-48cd-9702-93c8a9f3f2c7)

계층 구조로 보면 맨 아래부터 h/w -> virtualization layer -> virtual machine -> Linux, Windows, Solaris

<br/>

## Virtualization layer

**virtualization layer는 하드웨어 자원을 추상화하여, 여러 가상 머신이 동시에 사용할 수 있도록 함**

이것이 없으면 계층 구조를 못 쌓음 ! **즉, virtual machine을 사용하려면 반드시 설치 되어야 함**

host os가 이 기능(하드웨어 자원을 추상화하여, 여러 가상 머신이 동시에 사용할 수 있도록 해주는 것)을 하는 것이 아님

<br/>

## Booting and Bootstrap loader

**Booting: 컴퓨터를 켰을 때 커널을 메모리에 로드하여 운영 체제를 시작하는 절차**

**Booting 과정**

1. H/W 초기화 : CPU, 메모리, 입출력 장치 등 주요 하드웨어가 정상적으로 동작하는지 확인

2. Kernel을 메모리에 올리기 : 하드웨어 초기화가 완료되면, 운영 체제의 핵심 부분인 커널을 메모리로 로드

3. Kernel의 main 함수 첫 실행 : kernel에게 제어권을 넘겨줌

<br/>

**Bootstrap loader: 커널을 찾아 메모리에 로드하고 시작하는 작은 코드 조각**

컴퓨터가 켜지면 ROM에 저장되어 있는 Bootstrap가 실행하고 아래와 같은 기능을 수행함

<br/>

**Bootstrp 주요 기능**

1. 커널 위치 찾기: 저장된 커널의 위치를 확인합니다.

2. 커널을 메모리에 로드: 커널을 메모리로 복사

3. 커널 시작: 커널 실행을 시작시켜, 운영 체제의 제어권을 넘김

<br/>












































