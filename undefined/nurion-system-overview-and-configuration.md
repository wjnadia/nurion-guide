# 시스템 개요 및 구성

## **가. 개요**

KISTI 슈퍼컴퓨터 5호기 누리온(NURION)은 리눅스 기반의 초병렬 클러스터 시스템으로 이론 최고 성능(Rpeak) 25.7PFlops(4호기 Tachyon2의 약 70배)의 연산 처리 성능을 갖고 있습니다.

누리온은 1소켓(CPU)당 성능이 3TFlops(4호기 Tachyon2 전체 성능의 약 1/100)인 매니코어 CPU(68개의 코어로 구성) 8,305개로 구성되어 수십만 코어를 동시에 활용할 수 있는 클러스터 방식의 초고성능 컴퓨팅 시스템입니다. 그리고 고성능 인터커넥트(Interconnect), 대용량 스토리지, 버스트 버퍼(Burst Buffer)가 탑재되어 있습니다. 버스트 버퍼는 응용 프로그램에서 순간적으로 발생하는 대규모 I/O 요청을 원활히 처리 할 수 있습니다.

누리온은 이러한 대규모 계산 능력을 통해 국가 연구개발(R\&D)의 경쟁력 향상 기여에 목적을 두며, 기후 예측이나 신소재 개발 등 복잡한 문제나 신약개발, 항공 실험 등 실험적으로만 해결하기에는 위험하고 비용이 많이 소요되는 문제를 해결하는 데 기여하고자 합니다. 누리온은 이러한 과학기술 문제를 해결하기 위해 기획 단계부터 다양한 분야의 난제를 발굴하는 노력을 병행하고 있습니다.

또한 누리온은 이러한 연구 개발들을 지원하기 위한 다양한 종류의 소프트웨어를 탑재하고 지속적으로 업그레이드 하고 있으며, 고성능 하드웨어와 유기적인 연동을 통해 최고의 생산성을 유지하기 위해 노력하고 있습니다. 아울러 최적ㆍ병렬화를 비롯한 다양한 사용자 지원과 거대 문제 및 난제 해결 등을 위한 대형 과제 발굴을 통해서 국가 과학기술 발전과 지능정보사회 구현의 핵심 인프라로서 역할을 수행하고자 합니다.

![\[누리온 구성도\]](../.gitbook/assets/46cGZjtaR1zSlum.png)

![\[누리온 시스템 사양 및 구성\]](../.gitbook/assets/nurion-specification-configuration.png)



## 나. 계산 노드

누리온 시스템의 계산노드는 총 8,437개로 매니코어 기반의 Intel Xeon Phi 7250프로세서가 장착된 8,305개 계산노드와 Intel Xeon Gold 6148 프로세서가 장착된 132개 계산노드로 구성되어 있습니다.

### 1. KNL(매니코어) 노드

KNL 노드에 장착된 Intel Xeon Phi 7250 프로세서(코드명 Knights Landing)는 1.4GHz 기본 주파수에 68개 코어(hyperthreading off)로 동작합니다. L2 캐시 메모리는 34MB이며, 온패키지 메모리인 MCDRAM (Multi-Channel DRAM)은 16GB(대역폭 490GB/s)입니다. 노드 당 메모리는 96GB로 16GB DDR4-2400 메모리가 6채널로 구성되어 있습니다. 2U크기의 인클로저(enclosure)에는 4개의 계산노드가 장착되며, 42U 표준랙에 72개의 계산노드로 구성되어 있습니다.

![\[KNL 기반 계산노드 블록 다이어그램\]](../.gitbook/assets/pOeRBFHIcyQUwfC.png)

![\[KNL 기반 계산노드\]](../.gitbook/assets/MteLQQNt86MTMEz.png)

### 2. SKL(CPU-only) 노드

SKL(CPU-only) 노드에는 2개의 Intexl Xeon Gold 6148 프로세서(코드명 Skylake)가 장착되어 있습니다. 기본 주파수는 2.4GHz이며 20개의 CPU 코어(hyperthreading off)로 구성됩니다. L3 캐시 메모리는 27.5MB이며, 각 CPU당 메모리는 96GB(노드 당 192GB)로 16GB DDR4-2666 메모리가 6채널로 구성되어 있습니다. 2U크기의 인클로저(enclosure)에는 4개의 계산노드가 장착되어 있습니다.

![\[SKL 기반 CPU-only 노드 블록 다이어그램\]](../.gitbook/assets/NwiAvTQB3n1mbjQ.png)

![\[SKL 기반 CPU-only 노드\]](../.gitbook/assets/h3jV5a33UZiVL0I.png)



## 다. 인터커넥트 네트워크

노드 간 계산 네트워크 및 파일 I/O 통신을 위한 인터커넥트 네트워크로 인텔 OPA(Omni-Path Architecture)를 사용하고 있습니다. 100Gbps OPA를 사용하여 Fat-Tree 구조로 계산노드 간 50% blocking, 스토리지 간 non-blocking 네트워크로 구성 하였습니다. 계산노드와 스토리지는 277개의 48포트 OPA Edge 스위치에 연결되며 모든 Edge 스위치는 8대의 768포트 OPA Director 스위치에 연결 하였습니다.

![\[인터커넥트 네트워크 구성도\]](../.gitbook/assets/89LSApl4oE0nAN0.png)



## 라. 스토리지

### 1. 병렬파일시스템 및 버스트버퍼 구성

Nurion은 IO 처리 및 데이터 보관을 위해 병렬파일시스템과 버스트버퍼(Bust Buffer)를 제공합니다. 병렬파일시스템을 위해 스크래치(/scratch 21PB), 홈(/home01, 760TB), 어플리케이션(/app, 507TB) 세 개의 Lustre 파일시스템을 제공하고 있습니다.

각 파일시스템은 SFA7700X 스토리지 기반의 메타데이터 서버(MDS)와, ES14KX 스토리지 기반의 오브젝트 스토리지 서버(OSS)로 구성됩니다. 버스트버퍼는 계산 노드와 병렬파일시스템 사이에서 동작하는 NVMe 기반의 IO 캐시로 약 844TB의 용량을 제공합니다. Lustre 파일시스템은 계산노드, 로그인노드, 아카이빙 서버(Data Mover)에 마운트되어 IO 서비스를 제공합니다.

![\[병렬파일시스템 및 버스트버퍼 전체 랙 구성\]](../.gitbook/assets/sOdKlUWMwnbB9lP.png)

![\[PFS 서버 구성\]](../.gitbook/assets/UikUtB7HWx9PSti.png)

### 2. 버스트버퍼

#### 1) 개요

버스트버퍼(Burst Buffer, 이하 BB)는 계산노드와 스토리지 (/scratch) 사이의 I/O 가속화를 위한 캐시 레이어로 병렬파일시스템의 small I/O 또는 random I/O에 대한 낮은 성능 보완 및 병렬 IO의 성능 극대화를 위해 5호기에 새로이 도입되었습니다. I/O 의존성이 높은 사용자 어플리케이션의 성능 향상을 목표로 하고 있으며, KNL 노드를 사용하는 모든 큐에 대해 지원하고 있습니다.

![\[Burst Buffer 역할\]](../.gitbook/assets/6n7FDTWgDLwFPaD.png) ![\[Burst Buffer 서버 구성\]](../.gitbook/assets/ijCBgRkhSskY4Fv.png)

#### 2) 시스템 구성

BB 구성을 위해 DDN사의 IME240 솔루션이 적용되었으며, 위 \[Burst Buffer 서버 구성] 그림은 BB의 상세 구성을 나타냅니다.

|     **시스템**    | DDN IME240, Infinite Memory Engine Appliance |
| :------------: | :------------------------------------------: |
|  **소프트웨어 버전**  |              CentOS 7.4, IME 1.3             |
|  **최대 IO 성능**  |                    20 GB/s                   |
| **네트워크 인터페이스** |                    2 x OPA                   |
|   **SSD 타입**   |               1.2TB, NVMe 드라이브               |
|   **SDD 수량**   |       16ea(1.2TB NVMe) + 1ea(450GB SSD)      |
|   **용량(RAW)**  |                    19.2TB                    |

\[IME 단일노드 구성]

|   **IME240 x 48**  |     IME240 x 48     |
| :----------------: | :-----------------: |
|    **총 용량(RAW)**   |       979.2 TB      |
| **총 용량(패리티 적용 시)** | 816 TB (EC\*, 10+2) |
|    **최대 IO 성능**    |       800 GB/s      |

\[버스트버퍼 전체 구성]

* EC : Erasure Coding (설정은 변경될 수 있습니다)

{% hint style="info" %}
2022년 9월 22일에 마지막으로 업데이트 되었습니다.
{% endhint %}

