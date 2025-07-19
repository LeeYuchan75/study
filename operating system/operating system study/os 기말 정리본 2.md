## 10주차 

### Demand paging

**Demand paging** : 메모리 절약을 위한 기법으로, 필요한 페이지만 메모리에 올리는 방식

**Lazy swapper** : 페이지가 필요하지 않으면 절대 메모리에 가져오지 않는 방식

![IMG_3302](https://github.com/user-attachments/assets/d5dfb1ba-4fa6-45fb-b7ee-a690b714c3b7)

<br/>

### Valid & Invalid Bits

**Valid & Invalid Bits** :페이지마다 **해당 페이지가 현재 메모리에 있는지 아닌지**를 표시하는 비트

![IMG_3303](https://github.com/user-attachments/assets/66b864b8-1dd0-4a97-99fd-c572cdf3dcb3)

<br/>

### Page fault trap

**Page fault trap** : Invalid bit일 때 처리 과정을 설명

![IMG_3304](https://github.com/user-attachments/assets/fcfc1a07-d606-4fd8-9067-9523170d0549)

1. 참조

2. os가 page fault 감지 -> **page fault hander** 호출

3. 디스크(backing store)에서 해당 page가 존재하는지 확인

4. 디스크에서 해당 page를 가져옴

5. **page table 업데이트**를 하면 valid bit를 **v로 설정**

<br/>

### page falut 단점

page falut의 단점은 위 5가지 과정이 너무 오래 걸린다는 것이다

<br>

### Demand Paging 예시 : Pure paging

**Pure paging** : 페이지 기반 메모리 관리에서 처음에는 어떤 페이지도 미리 메모리에 올리지 않고, 실제로 접근될 때만 페이지를 로딩하는 방식

**참조(reference)되기 전까지는 절대로 swap-in하지 않는다** -> 프로그램을 시작할 때 메모리에 어떤 페이지도 올라와 있지 않음

<br/>

### Page Fault 시간 소요 계산 = EAT(Effective Access Time )

page fault 비율 p는 0 이상 1 이하의 값을 가짐

- p = 0이면 page fault 없음 (매우 이상적 상황)

- p = 1이면 모든 메모리 접근이 page fault 발생 → 최악의 상황

**Effective Access Time (EAT)** : 실제 접근 시간을 의미

![IMG_3305](https://github.com/user-attachments/assets/b9875255-a8af-4680-8c4f-df7204815c4c)

![IMG_3463](https://github.com/user-attachments/assets/3cecfb7a-8168-4353-ac56-2a395d745269)

<br/>

### 참조의 지역성(locality of reference)

page fault가 시간이 많이 소요돼도, 실제로 사용했을 때 문제가 없는 이유는 **page fault가 국소적으로 발생하기 때문**이다 -> **참조의 지역성(locality of reference)**

<br/>

### Page Replacement (페이지 교체)

**Page Replacement (페이지 교체)** : page fault가 발생했을 때 사용할 수 있는 빈 프레임이 없다면 현재 메모리에 있는 어떤 페이지 하나를 디스크로 내보내고, 그 자리에 새 페이지를 올리는 작업

<br/>

### Page Replacement (페이지 교체) 과정

1. 디스크에서 요청한 페이지의 위치를 찾는다

2. 빈 프레임이 있으면 그걸 사용하고, 없으면 페이지 교체 알고리즘을 통해 **희생될(victim 이라고 함) 프레임**을 선택

3. 해당 프레임에 요청한 페이지를 불러온다

4. 원래 시도했던 명령을 다시 실행한다 (page fault 복구 완료)

<br/>

### Modified Bit

**Modified Bit** : 해당 페이지가 **메모리 내에서 수정되었는지**를 나타내는 bit -> 수정이 되지 않으면 Disk/IO가 2번 발생할 일을 한번만 발생할 수 있도록 함 

![IMG_3307](https://github.com/user-attachments/assets/28584ad8-1fda-48b3-8884-b10e260c8f11)

### 기본 알고리즘 

**FIFO (First-In First-Out)** : 가장 먼저 들어온 페이지를 교체 -> **Belady’s Anomaly (벨라디의 모순)** : frame 늘렸더니 **오히려 page fault가 더 많아지는 현상**

**Optimal (OPT)** : 앞으로 가장 오랫동안 사용되지 않을 페이지를 교체 (**미래 정보 예상**, 이론적 기준) -> 예상할 수 없기 때문에 **LRU 알고리즘이 현실적인 대안**

LRU (Least Recently Used) : 가장 오랫동안 사용되지 않은 페이지를 교체 (**과거 정보 탐색**)

<br/>

### LRU 근사 알고리즘	

**Counter 방식** : 페이지마다 참조 시간 기록 → 가장 오래된 것 제거

**Stack 방식** : 최근 사용된 페이지를 스택 상단으로 이동

**Reference Bit 방식** : 페이지 참조 시 비트를 1로 설정 → 0인 페이지 우선 제거

**Additional Reference Bits** : 일정 시간마다 비트 시프트 → 과거 사용 이력까지 반영, **Reference Bit 방식으론 표현 범위가 적음** -> 이것을 해결한 것이 Additional Reference Bits이다, **이진수 값이 가장 작은 것을 victim으로 설정**

**Second-Chance (Clock Algorithm)** : 참조 비트가 1이면 기회를 한 번 더 줌

**Enhanced Second-Chance** : (Reference bit, Modify bit)의 4가지 조합 기준으로 교체 우선순위 결정 class1 (0,0) ~ class4 (1,1) **클래스가 낮을 수록 victim 선정**

LFU (Least Frequently Used) : 참조 횟수가 가장 적은 페이지 교체

MFU (Most Frequently Used) :  Frequently Used)	참조 횟수가 가장 많은 페이지 교체

<br/>

### LRU (Least Recently Used) algorithm 장단점

**LRU 장점** : 실제 시스템에서도 page fault를 줄이는 데 **좋은 성능**을 보인다

**LRU 단점** : 실제로 구현하려면 과거 참조 이력을 계속 추적해야 하므로 **구현이 매우 복잡**하다

<br/>

### 흐름 순서 

Thrashing	: 메모리 부족 → CPU 사용률 저하 -> **Locality model 모델을 사용하여 해결**

대표적인 Locality model : **Working Set Model**

Working Set 기반 정책	전체 프레임 수 < ∑WSS → Thrashing 발생

Allocating Kernel Memory (커널 메모리 할당) -> **Buddy System** (kernel 연속적인 공간 필요), **Slab Allocator** (kernel 내부에서 object 할당 시)

Buddy System -> **2의 거듭제곱 크기로 할당**

<br/>

### Slab Allocator 

- **낭비없이 메모리를 사용하기 위함**

- **slab** (하나 이상의 연속된 페이지로 이루어진 덩어리)

- **obect** (슬랩 안에 들어 있는 구조체 하나의 인스턴스),

- **cache** (같은 종류 object들을 저장하는 공간),

- **slab descriptor**(slab이 어디까지 사용되었는지 free가 몇개인지를 기록)

- **internal fragmentaion 발생 x** -> 슬랩 안 **객체 크기를 딱 맞게** 나눴기 때문

- 빠르게 메모리 요청을 만족시킨다

<br/>

## 11주차 

### FPP (the current file position pointer)

**FPP** : 현재 위치를 표현하는 포인터

<br/>

### 파일은 open 하는 이유 

- 파일 작업 시 디렉토리 탐색이 필요하기 때문
  
- open을 하면 운영체제가 그 파일 정보를 메모리에 저장해서 작업할 때마다 디렉토리를 계속 찾지 않아도 돼서 빠름

<br/>

### Open File Table

**Open File Table** : 파일을 열면 운영체제가 내부에서 그 파일에 대한 정보를 저장해두는 테이블 -> **inode를 저장**

이것을 기반으로 open을 해야하는 이유를 다시 설명하면 **file에 대한 inode 정보를 메모리에 올리기 위함**

<br/>

### Boot control block

**Boot control block** : 운영체제를 부팅하는 데 필요한 정보를 포함함

<br/>

### format

**format** : 디스크에 파일 시스템을 입혀서 운영체제가 사용할 수 있도록 준비하는 작

![IMG_3400](https://github.com/user-attachments/assets/8169e1a3-e5e4-43fe-b7cb-e8c24cf54f87)

<br/>

### 파일 시스템의 디렉터리 구조 (중요하다고 언급)

**디렉토리(directory)** : 파일 이름과 그에 대응하는 정보(inode 번호 등)를 저장하는 특별한 파일

<br/>

### 유닉스 디렉터리 구조 예시

![IMG_3399](https://github.com/user-attachments/assets/7f8d7c41-f400-4634-b358-28a009d5150f)

<br/>

### mount(마운트)

mount(마운트) : 디스크, USB, SD카드 같은 외부 저장장치를 운영체제의 디렉토리 트리 구조에 연결하는 작업

<br/>

### In-memory mount table 

**In-memory mount table** : 장착된(마운트된) 볼륨들에 대한 정보 -> 지금 어떤 파일 시스템이 마운트되어 있는지 여부 확인 가능

- **System-wide open-file table** : 열린 모든 파일에 대한 FCB(File Control Block) 복사본과 기타 정보 포함

- **Per-process open-file table** : 각 프로세스는 자신이 연 파일의 정보를 포인터로 system-wide table과 연결함

<br/>

### 파일을 열 때(open) 운영체제가 하는 일

1. 이 파일이 다른 프로세스에 의해 이미 열려 있는지 system-wide open-file table을 먼저 확인한다

2. 만약 이미 열려 있으면, 새로운 프로세스는 그걸 그대로 가리키는 포인터만 만들고 별도로 FCB(File Control Block)를 복사하지 않음

3. 만약 해당 파일이 아직 열려 있지 않다면, 디렉토리에서 파일명을 찾아야 함 (파일명 → inode 번호)

4. 그리고 나서 FCB(inode)를 복사해서 system-wide open-file table에 등록함

<br/>

### 파일 할당 방식 3가지 

- Contiguous allocation (연속 할당)

- Linked allocation (연결 할당) -> FAT(마이크로소프트가 사용)

- Indexed allocation (인덱스 기반 할당) -> Unix, Linux에서 사용

<br/>

### Contiguous allocation (연속 할당)

- 파일의 모든 블록을 디스크에서 연속된 공간에 저장하는 방식

- 시작 위치(block 번호)와 길이(블록 수)만 알면 됨

<br/>

### Contiguous allocation 단점

1. **외부 단편화 (External fragmentation)** : 디스크에 조각난 빈공간이 생겨서 연속 공간 확보가 어려움

2. **파일 확장 불가** : 중간에 다른 파일이 있으면 크기를 늘릴 수 없음

<br/>

### Linked allocation

- 포인터를 이용하여 서로 연속적이지 않아도 표현가능하게 함

![IMG_3407](https://github.com/user-attachments/assets/0542a862-cdd4-4837-b415-8be2ef49cb5e)

- **FAT (File Allocation Table)** : linked allocation의 구조는 유지하면서 포인터를 Block 내부에 저장하지 않고 **별도의 table로 관리** -> 마지막에 EOF(End of File)이 나올 때까지 찾아가는 방식 
  
<br/>

### Linked allocation 문제점 

- **매우 느림** : Direct access 일 때, 문제 발생 -> 계속 해당 block의 next block을 찾아야 함 (무식한 방식)

- **신뢰성 문제** : 해당 Block이 Bad Block (더 이상 사용할 수 없는 손상된 블록)이면 다음 정보를 찾지 못함 

<br/>

### indexed allocation

- 블록 위치를 **데이터 블록 안에 저장하지 않고**, 따로 **인덱스 블록을 하나 만들어서** 모든 블록 주소만 모아둔 것

- **index table** : 각 파일마다 고유한 인덱스 블록이 존재, 이 파일의 데이터 블록들이 어디 있는지 주소 목록이 들어 있음

![IMG_3410](https://github.com/user-attachments/assets/f1736762-671c-4c03-a506-b40d69246c0a)

<br/>

### indexed allocation 문제점

만약 파일이 1024개보다 더 많은 블록을 필요한 경우 인덱스 블록 하나로는 부족 -> **Multi-level index로 해결**

<br/>

### Multilevel index

- index table를 저장하는 index table을 만드는 것이다

![IMG_3413](https://github.com/user-attachments/assets/67b26d36-9e3b-4e20-8168-8cb1ad406e7d)

<br/>

### Multilevel index 문제점

**두 개의 인덱스 블록을 읽어야 한다** -> 번거로움 

<br/>

### Multilevel index 문제점을 LINUX, UNIX에서 해결한 방법

**인덱스 블록을 메모리에 유지**하면 이 문제를 완화할 수 있다

![image](https://github.com/user-attachments/assets/50b70ad6-57b8-4063-82fa-0e1c0212fec6)

![IMG_3416](https://github.com/user-attachments/assets/268ea82c-8174-464a-a02c-4e457795dad0)

<br/>

## 12주차 

### 디스크 접근 시간(access time)

디스크에서 데이터를 읽는 데 걸리는 시간은 **Seek time + Rotational delay + Data transfer time**

- Seek time : 디스크의 read/write 헤드가 원하는 데이터가 있는 실린더(cylinder) 로 이동하는 데 걸리는 시간

- Rotational delay : 디스크가 회전하여 원하는 섹터(sector)가 헤드 아래에 올 때까지 기다리는 시간

- Data transfer time : 데이터가 실제로 디스크에서 컴퓨터로 이동되는 시간

<br/>

### Disk bandwidth 

일정 시간 동안 **얼마나 많은 데이터를 전송할 수 있는지** 나타내는 지표 

<br/>

### Sustainable Bandwidth

장시간 동안 일관되게 유지되는 평균 전송 속도

<br/>

### Seek time이 증가하면 Bandwidth는 감소

<br/>

### SSD 

**SSD** : **플래시 메모리** 기반으로 데이터를 저장하는 저장장치

**SSD**는 **탐색 시간(Seek time)이나 회전 지연(Rotational latency)이 없음 -> SSD가 빠른 이유**


<br/>

### 플래시 메모리의 가장 큰 특징은 수명(life time)이 존재한다는 것이다

- **of bytes written (기록된 바이트의 총량)** : 플래시 메모리에 지금까지 얼마나 많은 데이터가 쓰였는지를 나타내는 지표 -> **수명과 관련이 있음**

- **Wear-Leveling (교수님이 중요하다고 강조)** : SSD의 모든 셀이 고르게 쓰이도록 분산시키는 기술 -> 임의의 셀만 계속 쓰이면 그 셀은 먼저 고장남 -> 수명이 과도하게 줄어드는 것을 방지

<br/>

### SSD 가장 큰 특징 

- 한 번 쓴 자리에 다시 **덮어쓰는(overwrite) 건 안 됨** -> 지웠다가 써야함

- 지울 수 있는 횟수가 **정해져 있음**

<br/>

### Garbage Collection (GC)

**Garbage Collection (GC)** : SSD에서 **더 이상 유효하지 않은(dead) 데이터들을 지우고**, **빈 공간(empty page) 을 확보**하는 자동 정리 과정

![IMG_3430](https://github.com/user-attachments/assets/409deb4b-e6f4-4544-a659-c9431f5d3674)

![IMG_3431](https://github.com/user-attachments/assets/c58afd08-6aed-48d1-8ea5-9274526b12f9)

































































































































































