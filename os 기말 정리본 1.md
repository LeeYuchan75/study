## 8주차 

### Deadlock(교착 상태)

**Deadlock(교착 상태)** : 여러 프로세스들이 **서로 자원을 점유**하고 있으면서 다른 프로세스가 가진 **자원을 기다리느라** 아무도 앞으로 진행할 수 없는 상태

<br/>

### Deadlock 해결 방법

1. **강제 종료(termination)** : 현재 교착 상태에 빠진 프로세스 중 하나를 강제 종료한다

2. **복구(rollback)** : 교착상태에 빠진 프로세스 중 하나의 자원을 강제로 빼앗아서(preempt) 해당 프로세스를 이전 상태로 되돌린다 & **check point Technic**

<br/>

### Resource Types

**Physical Resources (물리적 자원)** : 하드웨어에 직접 연결된 자원 (ex: CPU 사이클, 메모리 공간, 입출력 장치 (I/O devices))

**Logical Devices (논리적 장치)** : 실질적으로 소프트웨어적으로 관리되는 자원 (ex: 파일, 세마포어 (Semaphore))

<br/>

### instance

**instance** : 자원(resource) 종류 하나에 속하는 개별적인 개체

<br/>

### 자원을 사용할 때 프로세스의 순서 

- **Request (요청)** → 사용하려는 자원을 요청한다 (자원이 없다면 기다려야 한다)

- **Use(= hold) (사용)** → 자원을 얻으면 작업을 수행한다

- **Release (반납)** → 작업이 끝나면 자원을 반환한다

<br/>

### Hold & Request

**Hold & Request** : 프로세스가 **이미 하나의 자원을 점유**한 상태(hold = use) 에서, **추가로 다른 자원** 을 요청(request)하는 상황을 의미

<br/>

### Deadlcok 발생 가능성 조건 4가지 

1. Mutual Exclusion (상호 배제)

2. Hold and Wait (점유 및 대기)

3. No Preemption (비선점)

4. **Circular Wait (순환 대기)**

<br/>

### Deadlcok 100프로 발생 조건 

**위 4가지 조건 + 자원당 인스턴스가 하나일 때**

이것을 반대로 말하면, cycle이 생겨도 자원당 인스턴스가 여러개라면 Deadlock이 발생할 수도 있고 발생하지 않을 수도 있다

<br/>

### Deadlock을 다루는 방법

1. Deadlock이 아예 발생하지 않도록 한다

2. Deadlock이 발생하도록 놔두고, 나중에 복구(recovery) 한다

3. **Deadlock 문제를 무시한다 -> 리눅스, UNIX가 사용하는 방법**

<br/>

### 리눅스, UNIX가 사용하는 방법 : Deadlock 문제를 무시한다 

<br/>

### deadlock prevention

**deadlock prevention** : 이것은 Deadlock이 아예 발생하지 못하게, Deadlock 발생 가능성 조건 4가지 중 하나 이상을 깨버리는 전략이다

1. Mutual Exclusion 배제 불가

2. Hold and Wait **배제 가능** -> **자원 낭비 + 기아(starvation) 위험**

3. No Preemption 배제 불가

4. Circular Wait **배제 가능**

<br/>

### Deadlock Avoidance

전제조건 (Assumption) 

- 시스템은 각 프로세스가 앞으로 요청하고 해제할 리소스에 대한 **사전 정보**를 갖고 있어야 한다 -> Deadlock을 예방하기 위해 모든 프로세스가 요청할 리소스의 요청 및 해제의 완전한 시퀀스를 알고 있어야 함

- 각 프로세스는 자신이 필요로 할 수 있는 **각 리소스의 최대 개수**를 미리 시스템에 알려야 한다

<br/>

이것을 기반으로 **safe 여부 판단**

<br/>

### Deadlock 발생 가능성

**요청 수**가 가용 가능한 자원 수(인스턴스 수)보다 **더 많다면** 가능성 존재

다르게 말하면, 요청 수가 가용 가능한 자원 수보다 작다면, Deadlock이 절대 발생하지 않는다. 단 대기는 시킨

위에서 말한 Deadlock 발생 가능성 4가지 조건은 구조적 가능성이고 

이것은 수치적으로 발생할 수 있는 가능성이다 

<br/>

### safe state

**safe state** : 각 프로세스 Pᵢ가 필요한 자원이 현재 사용 가능한 자원 + 그 이전 프로세스들(Pⱼ, j < i)이 사용하던 자원으로 충족하는 상태

쉽게 말해 만약 Pᵢ가 지금 자원을 받지 못하더라도, 그보다 앞선 프로세스들(Pⱼ, j < i)이 먼저 종료되어 자원을 반환하면, 그 반환된 자원을 통해 Pᵢ는 필요한 자원을 받을 수 있다

<br/>

### 자원 할당 그래프(Resource-Allocation Graph)

**Resource-Allocation Graph(자원 할당 그래프)** : 단일 인스턴스(single instance) 자원 환경에서 데드락을 시각적으로 표현하는 방법

![image](https://github.com/user-attachments/assets/cc1d48e0-385a-4265-89da-9b2fb1d1f34b)

<br/>

### Banker’s algorithm

**Banker’s algorithm** : 자원의 **인스턴스의 수가 2개 이상**일 때 사용하는 알고리즘

![image](https://github.com/user-attachments/assets/57fcdb9e-b934-409a-a2e8-ee848aa0b1be)

<br/>

<br/>

### Deadlock avoidance & Deadlock Detection

**Deadlock avoidance** : Need = Max−Allocation (프로세스가 총 필요한 개수 - 현재 사용중인 개수) 최대 얼마까지 필요할지를 미리 계산하여 판단 

**Deadlock Detection (교착 상태 탐지)** : **이미 발생한 교착 상태가 있는지**를 시스템이 찾아내는 과정

**Wait-for Graph(대기 그래프)** : **단일 인스턴스에서만** Deadlock Detection(교착 상태 탐지)을 위해 사용하는 **시각적 표현 구조**

자원을 표시하지 않고 process만 화살표로 표시하여 어디서 교착상태가 발생했는지 한번에 알 수 있다

![image](https://github.com/user-attachments/assets/031f908a-6c60-44d8-b93d-95adc160570f)

<br/>

### Deadlock avoidance & Deadlock Detection 차이점 

**Deadlock avoidance**는 **미리 계산**을 하여 process를 할당하였다면, **Deadlock Detection**는 **추가를 하고 나서의 상황**을 본다는 차이점이 존재한다

<br/>

## 9-1 주차 

<br/>

### DRAM

**DRAM** : Dynamic RAM의 줄임말로 실행 중인 프로그램 코드와 데이터를 **실시간으로** 저장 및 CPU와 직접 통신을 담당

**DRAM을 사용하는 이유** : 디스크에서 데이터를 가져오는 것보다 **훨씬 빠른 속도**로 데이터를 읽고/쓰기 위해 사용

<br/>

### 메모리 계층 구조 (빠른 순서부터)

CPU 캐시 -> DRAM -> SSD/HDD -> 가상메모리 

<br/>

### virtual address space

**사용 이유** : 가상의 주소 공간을 사용하는 이유는 **더 많은 공간을 쓰기 위함**

<br/>

### address translation

**address translation** : Virtual Address Space에서 Physical Address Space로 바꿔서 이용해야 하는 과정 

<br/>

### MMU (시험 문제 예상)

**MMU (Memory Management Unit)** : CPU가 사용하는 가상 주소 (또는 논리 주소, Logical Address) 를 실제 메모리의 **물리 주소(Physical Address) 로 바꿔주는 하드웨어 장치**

**재배치 레지스 (relocation register)** 의 값을 더하는 원리

![image](https://github.com/user-attachments/assets/5d05ff07-c907-4c4d-a6c9-65342db06d6c)

<br/>

### 메모리 보호 (Memory Protection)

**메모리 보호 (Memory Protection)** : 각 프로세스가 자신에게 할당된 메모리 영역만 사용하도록 제한하는 것

![image](https://github.com/user-attachments/assets/ddda81fc-1544-4a4b-8fb9-b000551a435c)

실행할 프로세스를 선택 -> 커널이 선택된 프로세스에 맞게 base와 limit 레지스터 값을 업데이트

**Protection Bit 사용** -> Frame에 대한 접근 권한 관리

허가되지 않는 메모리 접근 -> **Segmentation Fault 발생**

<br/>

### Address Binding

**Address binding** : 변수나 코드가 실제 메모리에서 **어디에 위치할지** 결정하는 과정

![image](https://github.com/user-attachments/assets/635b635f-1523-498a-bfe8-ac47c8749175)

프로그램이 실행되기 전에, 코드 속 변수나 함수들이 Symbolic Address -> Relocatable Address -> Absolute Address 를 거쳐야 한다

<br/>

### 변수나 코드가 실제로 어느 메모리 주소에 있어야 할지 점점 확정되어 가는 과정

Symbolic Address (심볼 주소) -> Relocatable Address (재배치 주소) -> Absolute Address (절대 주소)

<br/>

### 주소 결합의 발생 시간

1. Compile time 문제점 : 시작 위치가 바뀌면 코드를 **다시 컴파일**해야 함 -> 전부 수정 필요

2. Load time 문제점 : 다시 실행할 때 **같은 위치 보장 안되기 때문에** 모든 값의 주소를 변경해야 함

3. Execution Time : 실시간으로 처리 -> **MMU가 이것을 해줌**

<br/>

### Memory Mapping Table(메모리 매핑 테이블)

**Memory Mapping Table(메모리 매핑 테이블)**  : CPU가 생성한 논리 주소(=가상주소)를 실제 물리 주소로 변환하기 위해 사용하는 **주소 변환 정보 구조체**

<br/>

### Dynamic Loading (동적 적재)

**Dynamic Loading** : **호출되지 않는 함수를 momory에 올리지 않는것**을 의미한다 라이브러리 자체에서 지원 -> **메모리 낭비 방지**

**os의 특별한 지원이 필요 없음. 라이브러리 수준에서 구현 가능** -> 라이브러리 형태로 제공됨

<br/>

### Dynamic Linking (동적 연결)

**Dynamic Linking (동적 연결)** : 링크(연결)를 실행 시간(run time) 에 수행한다 (ex: import math로 라이브러리를 불러오는 것)

Dynamic Linking은 실행 중 주소 공간 관리가 필요하므로 **OS의 개입이 필수**

<br/>

### Dynamic Loading -> os 개입 x 

### Dynamic Linking -> os 개입 o

<br/>

### stub 

- Dynamic Linking에서 연결할 함수 자리에 임시로 넣는 코드, **library와 어떻게 linking 할지에 대한 정보**가 들어

- stub는 가상 주소이지만, 진짜 함수 주소로 대체됨

<br/>

### Shared libraries

**Shared libraries** : **run time**에 임의의 메모리 주소에 로드되고, 메모리에 있는 프로그램과 연결될 수 있는 객체 모듈  -> 메모리 절약, 효율적

라이브러리에 업데이트가 일어날 경우 새 버전의 라이브러리로 자동 대체 가능 → **재컴파일 필요 없음**

<br/>

### Static library

개발자가 라이브러리의 최신 버전을 쓰고 싶다면, **반드시 프로그램을 다시 링크**해야 하는 문제점 존재 -> 이러한 문제 때문에 Static library는 거의 안 쓰고 Shared library를 자주 사용함

![image](https://github.com/user-attachments/assets/0a09c17b-1345-4b46-a1b4-4312b1a24da1)

<br/>

## 9-2 주차 

### Swapping

**Swapping** : 프로세스가 메모리에서 **backing store (백킹 스토어)** 로 일시적으로 이동되었다가, 다시 메모리로 복귀되어 실행을 계속하는 기법

<br/>

### Backing store (백킹 스토어)

**Backing store (백킹 스토어)** : **메모리에서 빠져나간 프로세스가 임시로 저장**할 수 있는 디스크 공간. 빠르게 접근할 수 있음 

<br/>

### Roll out, roll in (롤 아웃, 롤 인)

**Roll out, roll in (롤 아웃, 롤 인)** : **우선순위 기반 스케줄링 알고리즘**에서 사용되는 swapping 방식이다

<br/>

### Swapping 시간의 대부분은 데이터 전송 시간이다. 그리고 이 전송 시간은 스와핑되는 메모리의 크기에 비례한다 

즉, 많은 데이터를 스와핑하면 시간이 더 많이 걸리고, 적으면 시간이 덜 걸린다 

![IMG_3461](https://github.com/user-attachments/assets/c1b39c32-ca13-4bd1-8bee-e42841e6dfaa)

<br/>

### address translation

**address translation** : Virtual Address Space를 Physical Address Space로 바꾸는 것

<br/>

### address translation 작동 방식 3가지 

- Contiguous Memory Allocation

- Paging

- Segmentation

<br/>

### Contiguous Allocation

**Contiguous Allocation** : 하나의 프로세스가 메모리 내에서 연속된(block of contiguous) 물리적 공간에 할당되는 메모리 관리 방식

<br/>

### Contiguous Allocation 흐름 정리 

1. 프로세스가 메모리 요청

2. OS가 Hole을 탐색

3. 할당 전략 적용 : First-Fit / Best-Fit / Worst-Fit

4. 선택된 hole에 연속 공간 확보 

5. Relocation & Limit Register 설정 -> MMU에게 시작 주소(base), 허용 범위(limit)를 알려줌

6. 실행 중 → MMU가 주소 변환 수행

<br/>

### Contiguous Allocation cont'd : Dynamic Storage Allocation (동적 저장 공간 할당)

**Dynamic Storage Allocation** : 프로세스가 메모리를 요청할 때, 적절한 크기의 빈 공간(홀, Hole)을 찾아 할당하는 방법

ex: First fit, Best fit, Worst fit

<br/>

### External Fragmentation (외부 단편화)

**External Fragmentation (외부 단편화)** : 총 메모리 공간은 충분하지만, **연속적(contiguous)으로 존재하지 않아서** 사용할 수 없는 상황

ex: 10MB의 공간이 필요한데, 메모리에는 3MB, 4MB, 5MB처럼 나누어져 있을 때, 총합은 12MB이지만 연속적이지 않아서 할당할 수 없는 경우


<br/>

### External Fragmentation (외부 단편화) 해결 방법 

**Compaction (압축)** : 메모리의 조각난 공간(Hole)을 한 곳으로 모으는 작업

<br/>

### Compaction (압축) 조건

- **Relocation (재배치)가 동적**으로 이루어질 수 있어야 한다

- 그리고 **실행 시간 중에(Execution time)** 이루어져야 한다

- 즉, 프로세스의 위치를 변경할 수 있는 환경이어야만 압축이 가능

<br/>

### Internal Fragmentation (내부 단편화)

**Internal Fragmentation (내부 단편화)** : 할당된 메모리 블록이 실제 요청된 크기보다 약간 더 큰 경우, 그 남는 부분이 사용되지 않을 때 발생

ex: 5MB가 필요한데 메모리 블록 크기가 6MB로 할당되면, 1MB는 사용되지 않고 낭비됨

![IMG_3225](https://github.com/user-attachments/assets/d93d398f-4444-4b0e-9a74-2740d02ef996)

<br/>

![image](https://github.com/user-attachments/assets/f56752d5-45b1-416d-8186-367b5a562665)

<br/>

### Paging

**Paging** : 논리 주소 공간을 고정된 크기의 page로 나누고, 이를 물리 메모리 공간의 프레임(frame)에 **비연속적으로 매핑**하는 메모리 관리 기법

**페이지의 크기는 프레임의 크기와 동일해야한다**

**Internal Fragmentation (내부 단편화)** 발생하지만, **External Fragmentation (외부 단편화)는 없다**

<br/>

### Page Table (페이지 테이블)

**Page Table (페이지 테이블)** 논리 주소(logical address)와 물리 주소(physical address)를 **변환하는 매핑 정보**를 저장하는 테이블

<br/>

### Paging 과정 

![IMG_3227](https://github.com/user-attachments/assets/2b184551-4177-4a88-a3e6-340cb8a4c5d1)

<br/>

### Paging 주소 저장

![IMG_3462](https://github.com/user-attachments/assets/8634daa4-7ab0-481e-a5f9-65003af452e6)

<br/>

### Paging 사용을 위한 hardware 지원 : Register & TLB

### Register

1. **Page-table base register (PTBR)** : PTBR은 페이지 테이블의 **시작 주소(base address)** 를 가리킨다

2. **Page-table length register (PRLR)** : PRLR은 **페이지 테이블의 크기**를 나타낸다. 즉, 페이지 테이블이 **몇 개의 페이지 항목을 가지고 있는지**에 대한 정보를 가지고 있음

<br/>

### TLB

**TLB** : Associative Memory (연관 메모리)를 사용하는 하드웨어 캐시이다

<br/>

### TLB 목적 

페이지 테이블에서 주소를 매핑할 때 매번 메모리에 접근하면 시간이 오래 걸리므로, 최근에 참조한 페이지 번호와 프레임 번호를 **캐시에 저장하여 빠르게 찾을 수 있도록** 한다

<br/>

### TLB cont'd : ASID 

일부 TLB는 ASID (Address-space identifiers) 를 저장한다

**ASID** : **각 프로세스의 고유한 식별자(ID)로**, 서로 다른 프로세스가 **동일한 페이지 번호를 가지더라도 충돌 없이 매핑**할 수 있도록 해준다

<br/>

### TLB 과정 

![IMG_3231](https://github.com/user-attachments/assets/d4c1c911-afa7-4100-b40b-671047fce98c)

<br/>

### Associative Lookup

**Associative Lookup (ε (엡실론))** : TLB(Translation Lookaside Buffer)에서 페이지 번호를 찾는 시간

<br/>

### Hit Ratio 

**Hit Ratio (α, 알파)** : CPU가 요청한 논리 주소가 **TLB에서 바로 발견될 확률**을 의미한다

<br/>

### EAT 계산 방법

![image](https://github.com/user-attachments/assets/f4d5dd89-3b63-4a90-81f8-7f9fc36bc8d7)

<br/>

### Valid-invalid bit

**Valid-Invalid bit** : 페이지 테이블(Page Table)의 각 항목에 연결하여 페이지가 유효한지(Valid) 혹은 유효하지 않은지(Invalid) 를 나타냄

![IMG_3235](https://github.com/user-attachments/assets/e7148c82-67d5-4901-bac2-d38f89402a31)

<br/>

## 9-3 주차 

### Hierarchical Paging

**Hierarchical Paging** : 큰 주소 공간을 **효율적으로 관리하기 위해** 페이지 테이블을 **다시 작은 페이지 테이블로 나누는** 구조

<br/>

### Two-level page table 예시 

![IMG_3236](https://github.com/user-attachments/assets/c16bf539-e99f-4870-bb03-5d8dfbcee884)

![IMG_3237](https://github.com/user-attachments/assets/090530ee-02e7-4ce0-ba46-5de2944dcf6b)

<br/>

### Hashed Page Table

주소 공간이 32비트를 넘는 시스템에서 사용

페이지 번호를 해싱하여 테이블에 접근. 해시 충돌 해결을 위해 체인 구조 사용

![IMG_3289](https://github.com/user-attachments/assets/37648e7e-ff57-4736-9164-85bddbfc4db5)

<br/>

### Inverted page tables (역방향 페이지 테이블)

**사용 이유** : 페이지 테이블의 크기가 너무 크기 때문

**핵심 아이디어** : 모든 프로세스가 **하나의 공유 테이블을 사용하는 것**이 핵심

가상 페이지 기준이 아니라, **물리 메모리 기준으로 테이블 구성**된다 (물리 주소 → 해당 가상 주소가 누구의 것인지를 저장함)

![IMG_3291](https://github.com/user-attachments/assets/fd04c6cb-504e-408f-bd46-f1b4451f275c)

<br/>

### 리눅스에서 계층 구조 사용 과정 (시험 문제 예상)

![IMG_3297](https://github.com/user-attachments/assets/4f03ac96-018c-4a58-aca8-e3bd02a2411a)

![image](https://github.com/user-attachments/assets/6da34bd0-41a5-41e9-ba87-fa6ba2255864)

<br/>

### Segmentation

**Segmentation** : 메모리를 관리하는 방식 중 하나로, 사용자가 인식하는 논리적인 메모리 구조(= 사용자 시각) 를 반영한 방식

![IMG_3300](https://github.com/user-attachments/assets/9e63fb7e-f7f8-42b0-a228-29fe7793e0ed)

1. CPU가 논리 주소 (s,d) 생성 (s: 세그먼트 번호,  d = offset) + s < STBR 확인

2. s < STBR 를 만족하면, 세그먼트 테이블로 가서 base와 limit 값을 얻어옴 (by STBR)

3. offset의 길이를 base와 limit을 이용하여 비교한 뒤 사이에 존재하면 물리 주소로 계산 

<br/>

### Segment 보호 비트

**validation bit = 0** 이면 → 이 세그먼트는 불법적이므로 접근 금지

<br/>

### Segmentation 문제점

세그먼트는 **길이가 서로 다르기 때문에 단편화 문제 가능성**이 존재한다























































