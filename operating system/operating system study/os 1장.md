## 운영체제론(OS) 1장

## os의 정의 

os는 명확한 정의는 없지만 다음과 같은 의미와 역할을 가진다. 

1. os는 프로그램이다

2. os는 하드웨어를 관리한다

3. os는 프로그램의 실행을 조절한다

구글에서 검색 결과 정의는 다음과 같음 : 컴퓨터 하드웨어와 소프트웨어를 관리하고, 사용자와 컴퓨터 간의 인터페이스를 제공하는 시스템 소프트웨어

**하드웨어**란 컴퓨터를 구성하는 물리적인 장치(ex: cpu, 메모리, 하드디스크, HDD, SSD, 키보드, 마우스 등등 만질 수 있는 것)

**소프트웨어**란 하드웨어를 동작하게 만드는 프로그램과 데이터 (ex: 운영체제(os), 웹, 프로그래밍 언어 등등 만질 수 없는 것)

프로그램 수행 제어를 위해 하드웨어 관리가 중요하다 

<br/>

## 하드웨어(H/W)

하드웨어는 기본적으로 **CPU, memory, storage, I/O device** 로 구성됨

CPU: 중앙처리장치, 즉 CPU는 컴퓨터의 두뇌에 해당하는 부분으로, 프로그램의 명령을 실행하는 역할을 한다. CPU는 연산 처리, 제어 명령 실행, 프로그램 흐름 제어 등을 담당

memory: 컴퓨터가 데이터를 저장하고 빠르게 접근할 수 있도록 하는 공간, CPU가 실행할 명령과 데이터를 빠르게 읽고 쓸 수 있도록 **임시 저장하는 역할을 한다**

storage: 데이터를 영구적으로 저장할 수 있는 공간, (ex: HDD(하드디스크), SSD (솔리드스테이트디스크))

I/O device: 컴퓨터와 외부 세계(사용자 또는 다른 시스템) 간의 데이터 교환을 담당하는 장치

<br/>

## Storage structure

**주 메모리(Main Memory)**

RAM (휘발성): 실행 중인 프로그램과 데이터를 저장 (예: DRAM, SRAM)

ROM (비휘발성): 부팅 과정에서 필요한 기본 시스템 코드 저장

<br/>

**캐시 메모리(Cache Memory)**

CPU가 자주 사용하는 데이터를 저장하여 속도를 높임 (L1, L2, L3 캐시)

<br/>

**보조 저장 장치(Secondary Storage)**

하드디스크(HDD), SSD 등 데이터를 영구적으로 저장

<br/>

**가상 메모리(Virtual Memory)**

RAM이 부족할 때 디스크 공간을 임시 메모리로 사용 (스왑 공간)

<br/>

## Basic idea of the OS 

웹이나 프로그램이 하드웨어로 가려면 **반드시 os를 거쳐서 가야한다.** 앱이 바로 하드웨어에 접근할 수 없음

여기서 거쳐간다는 의미는 웹이 하드웨어로 접근하려면 os가 반드시 **system call**이라는 api를 제공해야한다

만약 모든 프로그램이 하드웨어에 직접 접근할 수 있다면, 악성 코드가 시스템을 쉽게 망가뜨릴 수 있어서 

시스템 콜을 사용하여 OS가 접근 권한을 제어해서 허용된 요청만 실행하도록 보호할 수 있음

따라서 os는 앱플리케이션 프로그램과 컴퓨터 하드웨어 중간에 존재한다 

<br/>

## system call and api

시스템 콜:  프로그램이 운영체제와 상호작용할 수 있도록 해주는 저수준 인터페이스

API: 프로그램이 다른 소프트웨어, 라이브러리와 상호작용할 수 있도록 해주는 고수준 인터페이스

즉, 시스템 콜은 api의 한 종류이다 

웹 개발을 할 때, api를 가져온다고 하는 것은 해당 웹이나 프로그램, 소프트웨어와 상호작용을 하여 데이터를 가져온다는 의미이다


<br/>

## The general roles of the OS 

**1.하드웨어 관리**

1. Access to I/O device (입출력 장치 접근 관리)

2. Access to files (파일 접근 관리)

3. Accounting (사용자 및 자원 사용 기록/관리)

4. Error detection (오류 감지 및 복구)

<br/>

**2.프로그램 실행**

1. Scheduling

2. Error reporting

위에서 핵심적인 부분은 Accounting과 Scheduling이다 

Accounting는 운영체제에서 자원 사용을 추적하고 기록하는 과정을 의미함. 이는 시스템 자원의 효율적인 관리와 공정한 배분을 위해 매우 중요하고, "자원"이라고 하면 주로 CPU 시간, 메모리, 디스크 사용, 입출력 장치 사용 등을 포함함

Scheduling은 프로그램 수행 순서를 결정 및 제어하는 역할 

따라서 os가 없다면 이러한 것들을 수행할 수 없음 

<br/>

## Objectives of the operating systems

1. Execute user programs and make it easier to solve user problems.

2. Make the computer system convenient to use.

3. Use the computer hardware in an efficient manner

<br/>

## OS의 역할 

 **1.OS is a resource allocator**

Manages all the resources(CPU time, memory space, file-storage space, I/O devices)

Decides **how to allocate** the resources to conflicting requests **for efficient and fair resource use**

 **2. OS is a control program**
 
**Controls the execution of programs** to prevent errors and improper use of the computer systems

<br/>

## Kernel

kernel은 os에서 핵심적인 부분으로 하드웨어 관리 및 시스템 제어를 한다. 

**os의 기능 중 하드웨어 관리와 시스템 제어는 바로 kernel에서 처리되는 것임**

기본적으로 os = kernel + 시스템 프로그램 + 응용 프로그램으로 구성되어 있음

<br/>

## 모든 시스템은 아래와 같이 구성되어 있다 

![System Resources](../images/operating%20system%20images/IMG_3505.jpg)

하나 이상의 CPU와 장치 컨트롤러가 공통 버스를 통해 연결되어 공유 메모리에 액세스할 수 있다.

메모리 사이클을 놓고 경쟁하는 CPU와 장치의 동시 실행

I/O device에서 얻은 데이터를 memory에 전송하고, 이것을 CPU애서 처리함

그 후, CPU에서 계산한 결과를 다시 메모리에 저장하고 I/O device로 전달하면 I/O device 에서 화면으로 표시함 

<br/>

## 컴퓨터 시스템에서 I/O 작동 방식

Each device controller is in charge of a particular device type (in charge of : 담당하다, 책임을 지다)

1. Each device controller has a **local buffer** ( local buffer 아래 설명 있음)

2. I/O: data is moved from/to main memory to/from local buffers

3. I/O devices and the CPU can execute concurrently

4. Why? DMA (Direct Memory Access)

5. Device controller informs CPU that it has finished its operation by causing an **interrupt**

Device controller 사용자가 키보드와 같은 입력 장치(input device)를 조작하면 Device controller 가 신호를 감지하여 디지털 데이터로 변환 후, os에 전달하는 역할을 한다 

이후 CPU에서 이것을 처리하고, 이것을 화면에 출력하거나 저장함

또한, interrupt는 어떤 장치가 다른 장치의 일을 잠시 중단시키고 자신의 상태 변화를 알려 주는 것을 의미한다 

<br/>

위에서 중요한 개념은 바로 **DMA**이다

DMA란 CPU를 거치지 않고, 입출력 장치(I/O 장치)와 메모리 간에 직접 데이터를 전송할 수 있는 기술이다

<br/>

## DMA 없는 경우 

I/O 장치와 메모리 간의 데이터 이동을 CPU가 직접 관리해야 한다

이 과정에서 CPU는 데이터가 이동될 때마다 직접 제어해야 하므로, I/O 작업의 속도가 CPU의 처리 속도에 따라 영향을 받게 된다

I/O 작업을 처리하는 동안 CPU는 시간을 낭비할 수 있고, 즉, CPU가 입출력 작업을 완료할 때까지 기다려야 하므로 효율성이 떨어진다

또한, CPU가 데이터 전송 작업을 모두 처리해야 하므로, 다른 계산 작업을 수행하는 데 시간을 소모하게 된다

정리하면 **DMA가 없는 경우 CPU는 계산, 데이터 전송**을 함 

<br/>

## DMA가 존재하는 경우

만약 DMA가 존재한다면, CPU의 데이터 전송 부담을 줄어줌

즉, DMA의 역할은 CPU 없이 입출력 장치와 메모리 간에 데이터를 직접 전송할 수 있도록 하여 CPU가 데이터 전송을 관리하지 않아 시스템 전체 성능을 크게 향상시킴 

DMA가 데이터 전송을 완료한 후, 인터럽트를 통해 CPU에 완료를 알리고, CPU는 후속 작업을 처리한다 

정리하면 DMA는 CPU의 부담 감소와 전체적인 시스템 속도 향상에 큰 기여를 함 

<br/>

## local buffer

local buffer 란 장치 컨트롤러가 입출력(I/O) 작업을 수행할 때 데이터를 임시로 저장하는 메모리 공간이다. 

main memory에서의 역할도 임시 저장인데 굳이 local buffer를 사용하는 이유는 **입력 데이터를 처리하는 과정에서 속도 차이를 해결하기 위해서다**

입력 장치(input Device)인 키보드로 입력하는 과정을 예로 들자면, 사람이 타이핑하는 속도는 매우 느리지만, CPU는 키 입력을 처리하는 속도가 훨씬 빠름(초당 수십억 회 연산 가능)

만약 CPU가 키 입력을 실시간으로 처리한다면, 사람이 키를 누를 때까지 CPU가 멈춰야 해서 **매우 비효율적이다**

이것을 해결한 것이 local buffer이다. 키보드를 눌렀을 때 입력 받은 데이터가 local buffer 에 임시 저장되고, CPU는 이것을 적당한 주기를 설정하여 local buffer에서 데이터를 가져와 처리해주고 다시 남은 시간에 자기 일을 한다.

이렇게 되면, 효율성과 전체적인 속도가 매우 향상이 된다

<br/>

## ISR(interrupt service routine)

ISR :  인터럽트가 발생했을 때 실행되는 코드(핸들러)

**ISR의 역할**

1. 인터럽트 원인 확인 (예: 키보드 입력, 디스크 I/O 완료 등)

2. 필요한 데이터 처리 (예: 입력 값을 버퍼에 저장, 파일 읽기 완료 등)

3. 인터럽트 종료 후 원래 작업 복귀

<br/>

## interrupt, Trap

Interrupt transfers control to the interrupt service routine generally, through the interrupt vector, which contains the addresses of all the service routines.

Interrupt architecture must save the address of the interrupted instruction.

An operating system is interrupt driven.

e.g.) timer interrupt

<br/>

<해석 및 정리>

interrupt는 일반적으로 모든 서비스 루틴의 주소를 포함하는 **interrupt vector**를 통해 **ISR(Interrupt servjce routine)** 에 제어권을 전송한다 (ISR는 unconditionally, imediately하게 시행함)

여기서 interrupt vector란 ISR로 가기 위한 주소 테이블이다

interrupt 아키텍처는 중단된 명령어의 주소를 저장해야 한다

운영 체제는 interrupt 기반으로 작동된다 -> interrput가 없으면 CPU가 계속 감시해야함. 하지만 interrupt로 알려주면 필요할 때만 처리할 수 있어서 효율적임

예) timer interrupt -> 가장 많이 발생하는 interrupt

<br/>

Trap : 프로그램 실행 중 발생하는 이벤트에 의해 발생하는 것.

즉 하드웨어에서는 interrupt로 표현했다면, 소프트웨어에서는 Trap으로 표현함 -> interrupt와 Trap은 쓰이는 위치(하드웨어, 소프트웨어)는 다르지만 역할은 같음 

<br/>

Interrupt와 Trap의 차이는 위치 말고도 비동기식과 동기식이라는 차이점이 있다

Interrupt : 현재 실행 중인 명령어와 관계없이 **외부에서** 발생 CPU가 특정 작업을 실행하는 도중, 갑자기 외부 장치(키보드, 디스크 등)가 인터럽트를 보내서 언제 발생할지 예측할 수 없음 -> 비동기식

Trap : 현재 실행 중인 명령어의 결과에 의해 발생하고 항상 특정 명령어가 실행될 때만 발생하므로 예측 가능 (ex: system call, Segmentation Fault) -> 동기식




<br/>

## Interrupt-Driven I/O 과정 (interrupt 기반 I/O 과정)

1. device driver initiates I/O 

2. initiates I/O

3. input ready, output complete. or error generates interrupt signal

4. CPU receiving interrupt, transfers control to interrput handler

5. interrupt handler preocess data, returns from interrupt

6. CPU resumes processing of interrupted task

<br/>

<해석 및 정리>

1. 장치 드라이버가 I/O 요청 

2. 장치 컨트롤러가 I/O 수행

3. I/O 완료 후 인터럽트 발생 

4. CPU가 인터럽트 감지, ISR 실행 

5. ISR이 데이터 처리 후 인터럽트 종료

6. CPU가 원래 코드로 복귀, 실행 계속

이 방식 덕분에 CPU는 I/O를 기다리지 않고 다른 작업을 수행할 수 있음

<br/>

또한 위 과정에서 기존 코드를 수행하다가 Interrupt가 발생하면 그것을 처리하고 다시 기존 코드로 돌아오려면

ISR로 가기 전에 해당 위치의 주소를 저장해야함 

<br/>

![Image](https://github.com/user-attachments/assets/99e4d040-5f25-44e9-ba3c-a1cc293feb21)

<br/>

## Device controller, Device driver

Device Controller: 실제 하드웨어를 제어하는 물리적인 장치

Device Driver: OS와 하드웨어(장치) 사이의 소프트웨어

<br/>

## Cache

Cache : **자주 사용되는 데이터를 빠르게 접근할 수 있도록 하기 위한 임시 저장소** , CPU와 메모리, 디스크 등 다양한 저장 장치 간의 속도 차이를 해소하는 데 사용된다 

Cache와 local buffer와 다른 점은 Cache는 주로 사용되는 데이터나 명령어를 빠르게 접근 할 수 있음(사용 범위: 즉 컴퓨터의 전체적인 부분의 향상을 기여함). local buffer는 오직 I/O 에서의 성능만을 향상시킨다는 차이가 있음 

<br/>

## How to access storage medium

저장 매체에 접근하는 방법은 

1. **빠른 저장소(캐시)** 부터 정보가 있는지 확인 -> 데이터를 빠르게 접근하기 위함 

2. 캐시에 데이터가 존재하면, 그 정보를 빠르게 사용 가능 -> 캐시에서 데이터를 찾은 상황을 "Cache hit" 라고 함

3. 캐시에 데이터가 없으면,  메인 메모리나 저장소(디스크)에서 데이터를 가져와 캐시에 복사한 후, 캐시에서 사용함 -> 복사라는 것은 데이터를 저장한다는 말과 동일

<br/>

또한 Cache는 Cache로 데이터가 저장되는 매체(ex: CPU, 디스크 등등)보다 용량이 작다 

**캐시의 용량은 제한적**이므로, 모든 데이터를 저장할 수 없기 때문에 자주 사용되는 데이터를 빠르게 저장하여 성능을 최적화함

따라서 Cache의 관리가 중요하고, 또한 크기 및 교체를 적절하게 해야한다 

<br/>

## Computer systems architecture

Most systems use a single general-purpose processor (PDAs through mainframes)

<해석 및 정리>

대부분의 시스템은 단일 범용 프로세서를 사용 일반적으로 컴퓨터 시스템(예: 스마트폰, 노트북, 서버 등)은 하나의 범용 프로세서(general-purpose processor) 를 사용함.

PDA(Personal Digital Assistant)부터 메인프레임(Mainframe)까지 모든 시스템이 단일 프로세서를 기본으로 사용한다는 의미 (PDA: 스마트폰 이전 시대의 휴대용 전자 기기, Mainframe: 대형 중앙 컴퓨터로, 수천~수백만 개의 작업을 동시에 처리)

대부분의 시스템은 또한 특수 목적 프로세서도 가지고 있다

또한 
<br/>

Multiprocessors systems growing in use and importance

<해석 및 정리>

대부분의 시스템에는 특수 목적 프로세서도 포함됨

일반적인 CPU 외에도 특정 기능을 수행하는 특수 목적 프로세서(special-purpose processor) 가 존재

<br/>

Multiprocessor 장점 

1. **Increased throughput** : 많은 작업을 빠른 시간 내에 처리할 수 있지만 프로세서(CPU)가 N개 있다고 해서 **속도 향상이 정확히 N배가 되는 것은 아니라 N배보다 좀 더 낮아짐**, 모든 작업이 완전히 독립적인 것이 아니고, 일부 작업은 이전 작업의 결과를 기다려야 실행될 수 있기 때문

2. **Economy of scale** : 더 많은 프로세서를 추가해도 비용 대비 성능이 좋아지는 효과

3. **Increased reliability** : 멀티프로세서 시스템에서는 한 개의 프로세서가 고장 나더라도 전체 시스템이 멈추지 않음 -> 신뢰성 향상

<br/>

## Two types of multi-processor systems

## 1. Asymmetric multiprocessing (비대칭 멀티프로세싱)

하나의 **master processor(주 프로세서)** 가 있고, **다른 프로세서들은 슬레이브 프로세서**로 작동함

master processor 는 전체 시스템의 메모리 맵에 접근할 수 있고, 다른 프로세서들은 마스터의 지시에 따라 작업을 수행한다 

작동방식 : 마스터 프로세서가 시스템을 제어하고, 나머지 프로세서는 마스터의 지시를 받으며 작업을 처리함

슬레이브 프로세서는 보통 **자신만의 메모리를 가지고 있으며**, 이 메모리는 주 **프로세서의 메모리와 연결되지 않음**

<br/>

## 2. Symmetric multiprocessing (대칭 멀티프로세싱)

**모든 프로세서가 동등한 권한을 가지며**, 마스터-슬레이브 관계가 없다

각 프로세서가 **메모리를 공유**하고 서로 **직접 상호작용할 수 있다**

<br/>

## Multiprocessor memory model

**1. UMA (Uniform memory access)**

**모든 CPU가 메모리에 동일한 속도로 접근**할 수 있음. 공유된 단일 메모리(Shared Memory)를 사용. SMP (Symmetric Multiprocessing) 시스템에서 주로 사용됨

장점: 프로그래밍이 단순함 (메모리 접근 속도가 일정하므로). 캐시 일관성 유지가 쉬움

단점: CPU 수가 많아지면 메모리 대역폭이 병목이 될 수 있음 (병목: 시스템 성능을 제한하는 요소)

<br/>

**2. NUMA (Non-Uniform Memory Access)**

**CPU가 접근하는 메모리 위치에 따라 속도가 다름.** 각 프로세서가 **자신의 로컬 메모리(Local Memory)** 를 가지며, 다른 프로세서의 메모리(원격 메모리)에 접근할 수도 있음.

장점: 확장성이 뛰어나며 많은 CPU를 연결 가능. 병목 현상이 줄어들어 성능이 향상됨 (각 CPU에 로컬 메모리를 분배하여 병목 현상을 줄이기 때문)

단점: 프로그래밍이 복잡해짐 (로컬/원격 메모리를 고려해야 함). 캐시 일관성 문제 발생 가능.


![Image](https://github.com/user-attachments/assets/eb15fb4f-74b0-4542-966f-59649a133e4c)

<br/>

**위 이미지: UMA , 아래 이미지: NUMA**

<br/>

## 멀티 코어(Multi-Core) 

하나의 프로세서(칩) 안에 여러 개의 CPU 코어를 포함하는 기술

멀티 프로세서의 발열 문제를 어느정도 해결하여 많이 사용되고 있음 

<br/>

## Multiprogramming

정의: CPU와 I/O 장치를 항상 바쁘게 유지하기 위해 여러 개의 프로그램을 메모리에 올려두고 실행하는 기법

**목적: CPU와 I/O 장치를 최대한 활용하여 낭비되는 시간을 최소화하기 위함**

동작 방식 

1. multi programming은 작업(코드와 데이터)을 정리하여 CPU가 항상 실행할 작업을 갖도록 함

2. 메모리에 여러 개의 작업을 보관 → 한 번에 전체 작업을 실행하는 것이 아니라, 일부만 로드함.

3. Job Scheduling을 통해 실행할 작업을 선택함.

4. 어떤 작업이 I/O 작업을 수행하느라 대기 상태가 되면, OS가 즉시 다른 작업으로 전환(Switching)하여 CPU를 활용함.

<br/>

## Some related concepts

1. CPU Scheduling : 여러 개의 프로세스가 동시에 실행 준비가 되어 있을 때, CPU가 어떤 프로세스를 먼저 실행할지 결정하는 과정

2. Job Scheduling : 여러 개의 작업이 실행 준비가 되어 있지만, 메모리에 올릴 공간이 부족할 경우, 어떤 작업을 메모리에 올릴지를 결정하는 과정

3. Swapping : 물리 메모리에 프로세스를 모두 수용할 수 없을 때, 실행을 위해 프로세스를 메모리에서 디스크로 내보내거나 다시 불러오는 기법. 과거에는 전체 프로세스를 내보내는 방식이었지만, 현대 OS에서는 **부분적으로만 교체하는 기법(페이징, 세그먼테이션)** 을 주로 사용합니다.

4. Virtual Memory : 프로세스의 모든 데이터가 한 번에 메모리에 올라가지 않아도 실행할 수 있도록 하는 기술 ex) 책을 읽을 때, 책 전체를 한 번에 펼쳐놓을 필요가 없음. 필요한 몇 장(페이지)만 책상 위에 펼쳐놓고, 나머지는 책장에 두고 필요할 때 꺼내서 보면 되는 것처럼 Virtual Memory도 같은 원리로 작동됨

<br/>

## dual-mode

컴퓨터에서 실행되는 프로그램은 두 가지 모드 중 하나에서 실행됨

1. user mode : 사용자 프로그램이 실행되는 모드. 제한된 권한 (일반적인 애플리케이션 실행)

2. kernel mode : 운영체제(OS)가 실행되는 모드. 모든 명령 실행 가능 (시스템 제어)

쉽게 말하면 

uesr mode는 사용자가 실행하는 일반 프로그램 (예: 웹브라우저, 게임 등)

kernel mode는 운영체제가 시스템을 관리하는 모드 (예: 파일 시스템, 하드웨어 제어 등)

<br/>

**Mode Bit** : CPU가 현재 실행 중인 모드(uesr or kernel mode)를 구별하는 하드웨어 비트

Kernel Mode (0) → OS의 핵심 기능을 수행 (모든 명령 실행 가능)

User Mode (1) → 제한된 명령만 실행 가능 (안전성 확보)

<br/>

예를 들어 

유저 모드에서 실행 중인 프로그램은 직접 CPU나 메모리를 조작할 수 없음 만약 사용자가 프린터를 사용하려 하면 아래의 과정을 거친다

1. 유저 모드 

2. OS에게 요청

3. OS가 커널 모드에서 처리

4. 결과 반환

<br/>

운영체제는 유저 모드와 커널 모드를 구분하여 시스템을 보호함.

시스템을 보호해야 하는 이유

1. 사용자가 실수로 시스템을 망가뜨리는 것을 방지

2. 악성 프로그램(바이러스, 해킹)이 시스템을 직접 조작하는 것을 막음

또한 **Privileged Instructions(특권명령)** 은 운영체제(OS)에서만 실행할 수 있는 명령어로, **Kernel Mode에서만 실행 가능하며**, User Mode에서는 실행이 제한됨.

유저 모드에서 특권 명령을 실행하려 하면, 하드웨어가 이를 차단하고 실행되지 않음. 이때 **예외(Trap) 또는 인터럽트(Interrupt)** 가 발생하여 운영체제가 개입하고, 이렇게 함으로써 사용자가 임의로 시스템을 조작하는 것을 방지함

![Image](https://github.com/user-attachments/assets/85174758-7d66-4327-9f69-633566cba31d)













































