**Volume 16 Compute and AI Architecture**

# Chapter 04. Edge PC

## 04.01. Intel NUC/Mini-ITX Selection

![](images/image1.png){width="7.268055555555556in" height="7.268055555555556in"}

인텔 NUC(Intel NUC) 또는 미니 ITX(Mini-ITX) 플랫폼을 로봇 엣지 PC(Robotics Edge PC)로 선정할 때는 전체 컴퓨팅 아키텍처(Compute Architecture)에서 해당 컴퓨터가 담당할 역할을 먼저 정의해야 한다. 결정론적 제어(Deterministic Control)를 담당하는 MCU나 임베디드 AI 추론(Embedded AI Inference)에 최적화된 젯슨(Jetson)과 달리, 엣지 PC(Edge PC)는 일반적으로 상위 수준 인지(Perception), 위치추정(Localization), 매핑(Mapping), 데이터 처리(Data Processing), 진단(Diagnostics), 시각화(Visualization), 미들웨어(Middleware), 감독 애플리케이션(Supervisory Application)을 실행한다.

인텔 NUC급 시스템(Intel NUC-class System)은 설치 공간, 개발 속도, 소프트웨어 호환성이 중요한 로봇에 적합한 소형 고집적 컴퓨팅 플랫폼(Compact Integrated Computing Platform)을 제공한다. CPU, 메모리 인터페이스(Memory Interface), 저장장치(Storage), 네트워크(Networking), USB 연결 및 그래픽 기능(Graphics Function)이 작은 인클로저(Enclosure) 또는 보드급 패키지(Board-level Package)에 통합되어 기계적 통합 부담을 줄이고 리눅스(Linux), ROS 2, 컨테이너(Container), 기존 x86 소프트웨어를 신속하게 적용할 수 있다.

미니 ITX(Mini-ITX) 플랫폼은 프로세서(Processor), 메인보드(Motherboard), 메모리(Memory), 저장장치(Storage), 네트워크(Networking), 전원공급장치(Power Supply), 냉각 시스템(Cooling System), 확장 장치(Expansion Device)를 독립적으로 선정할 수 있어 높은 아키텍처 유연성(Architectural Flexibility)을 제공한다. 표준 170 × 170 mm 메인보드는 대부분의 NUC급 솔루션보다 크지만 PCIe 확장, 대용량 메모리, 다중 NVMe, 외장 GPU(Discrete GPU), 네트워크 어댑터(Network Adapter), 프레임 그래버(Frame Grabber), 로봇 전용 인터페이스 구성에 훨씬 높은 자유도를 제공한다.

따라서 첫 번째 선정 기준은 물리적인 크기보다 워크로드(Workload)가 되어야 한다. 내비게이션(Navigation), ROS 2 노드(Node), 경량 인지(Lightweight Perception), 플릿 통신(Fleet Communication), 로깅(Logging), 운영자 인터페이스(Operator Interface)를 실행하는 로봇은 최신 NUC급 프로세서로 충분할 수 있다. 반면 다중 카메라 처리(Multi-camera Processing), 대규모 포인트 클라우드(Point Cloud) 연산, 고해상도 매핑(High-resolution Mapping), 센서 기록 또는 GPU 가속 인지(GPU-accelerated Perception)를 수행한다면 미니 ITX가 제공하는 높은 메모리 용량과 PCIe 대역폭, 열설계 범위가 필요할 수 있다.

프로세서 선정에서는 단시간 벤치마크(Benchmark) 성능보다 지속 성능(Sustained Performance)을 고려해야 한다. 로봇 워크로드는 카메라(Camera), 라이다(LiDAR), 레이더(Radar), GNSS 및 진단 데이터를 입력받으면서 수 시간 이상 연속 실행되는 경우가 많다. 높은 터보 주파수(Turbo Frequency)를 지원하는 프로세서도 초기에는 높은 성능을 보이지만 인클로저 내부 온도가 상승하면 성능이 감소할 수 있으므로, 실제 로봇의 예상 주변 온도와 냉각 조건에서 안정적인 지속 처리량(Sustained Throughput)을 확보하는 것이 중요하다.

메모리 용량(Memory Capacity)과 메모리 대역폭(Memory Bandwidth)은 엣지 PC의 동작 성능에 직접적인 영향을 준다. ROS 2 프로세스, 인지 파이프라인(Perception Pipeline), SLAM, 지도 데이터베이스(Map Database), 컨테이너, 시각화 도구 및 로깅 서비스가 동시에 실행되면서 메모리를 공유할 수 있다. 따라서 향후 소프트웨어 증가를 고려한 충분한 여유 용량을 확보해야 하며, 중간 수준의 메모리로 충분하다면 NUC가 적합하고 대용량 메모리 또는 다수의 고대역폭 애플리케이션이 필요하다면 미니 ITX가 유리하다.

저장장치 아키텍처(Storage Architecture)는 단순한 부가 구성요소가 아니라 컴퓨팅 설계(Compute Design)의 일부로 다루어야 한다. NVMe SSD는 센서 데이터 기록, 지도 접근, AI 모델 로딩(AI Model Loading), 소프트웨어 배포에 높은 처리량을 제공하지만 지속적인 데이터 기록은 상당한 발열과 쓰기 내구성(Write Endurance)을 요구한다. 대규모 데이터를 지속적으로 수집한다면 시스템 드라이브(System Drive)와 데이터 드라이브(Data Drive)를 분리하여 입출력 경합을 줄이고 유지보수, 복구 및 교체 절차를 단순화할 수 있다.

PCIe 기능은 소형 NUC 시스템과 미니 ITX 아키텍처를 구분하는 가장 중요한 요소 중 하나이다. 로봇 플랫폼에는 추가 이더넷 컨트롤러(Ethernet Controller), CAN 인터페이스, GPU 가속기(GPU Accelerator), GMSL 프레임 그래버, 고속 저장장치 또는 특수 데이터 수집 카드가 필요할 수 있다. 이러한 장치가 제품 수명주기(Product Lifecycle) 동안 추가될 가능성이 있다면 메인보드 선정 전에 PCIe 레인 수(Lane Count), 슬롯 구성(Slot Configuration), 세대(Generation), 대역폭 할당(Bandwidth Allocation), 기계적 장착 공간을 평가해야 한다.

엣지 PC가 고대역폭 센서의 데이터 집선 지점(Data Aggregation Point) 역할을 하는 경우가 많기 때문에 네트워크 아키텍처(Network Architecture)도 중요하다. 다수의 기가비트 이더넷 카메라(Gigabit Ethernet Camera), 3D 라이다, 외부 컴퓨팅 모듈 및 플릿 통신 링크가 동시에 상당한 트래픽을 발생시킬 수 있다. 듀얼 이더넷(Dual Ethernet)은 센서 네트워크와 외부 네트워크를 분리하는 데 유용하며 여러 고속 장치가 동시에 동작한다면 2.5GbE, 5GbE 또는 10GbE가 필요할 수 있다.

USB 연결은 시제품(Prototype) 통합을 단순화할 수 있지만 양산 로봇(Production Robot)에서는 커넥터 고정력(Connector Retention), 케이블 내구성(Cable Robustness), 장치 인식(Enumeration), 순간적인 전원 이상 이후의 복구 특성을 검토해야 한다. USB 카메라, GNSS 수신기, 개발 인터페이스 및 진단 장치는 엔지니어링 단계에서 편리하지만 핵심 양산 센서에는 이더넷, 자동차용 인터페이스(Automotive Interface), 또는 기계적으로 고정되는 산업용 커넥터(Industrial Connector)가 더 적합할 수 있다. 따라서 단순한 포트 개수만으로 플랫폼을 선정해서는 안 된다.

전원 아키텍처(Power Architecture)는 로봇의 배터리 시스템(Battery System)과 함께 평가해야 한다. 상용 NUC 제품은 일반적으로 안정화된 DC 어댑터(Regulated DC Adapter)를 전제로 하지만 이동 로봇에서는 배터리 전압 변동, 모터 기인 과도현상(Motor-induced Transient), 회생 에너지(Regenerative Event), 기동 시 전압 변동 및 갑작스러운 전원 차단이 발생할 수 있다. 따라서 적절한 안정화 전원단(Regulated Power Stage), 보호 회로(Protection Circuit), 점화 제어(Ignition Control), 제어된 종료(Controlled Shutdown) 전략을 함께 구성해야 한다.

열설계(Thermal Design)는 이론적인 컴퓨팅 성능을 실제 현장에서 지속적으로 유지할 수 있는지를 결정한다. NUC 시스템은 고집적 냉각 구조를 통해 소형화를 달성하는 반면 미니 ITX는 더 큰 방열판(Heat Sink), 팬(Fan), 덕트(Duct), 섀시 수준 공기 흐름(Chassis-level Airflow)을 적용할 수 있다. 실외, 밀폐 공간, 모터나 전력전자장치 주변에서 운용되는 로봇은 주변 온도, 내부 열 재순환, 먼지 축적, 팬 성능 저하 및 열 스로틀링(Thermal Throttling)을 함께 분석해야 한다.

기계적 신뢰성(Mechanical Reliability) 역시 소비자용 PC와 로봇용 엣지 컴퓨터를 구분하는 중요한 요소이다. 이동 로봇에서는 진동(Vibration), 충격(Shock), 반복 가속, 커넥터 움직임 및 지속적인 기계적 가진(Mechanical Excitation)이 발생한다. 메모리 모듈, NVMe 장치, PCIe 카드, 방열판 및 케이블은 전체 운용 수명 동안 안정적으로 고정되어야 한다. 미니 ITX는 높은 패키징 자유도를 제공하지만 그만큼 구조 고정과 진동 설계에 대한 책임도 시스템 설계자에게 증가한다.

소프트웨어 호환성(Software Compatibility)은 x86 엣지 PC의 주요 장점이다. 표준 리눅스 배포판(Linux Distribution), ROS 2 패키지, 개발 도구(Development Tool), 가상화 기술(Virtualization Technology), 컨테이너 런타임(Container Runtime), 데이터베이스(Database), 시각화 소프트웨어 및 다양한 산업용 SDK를 활용할 수 있다. 따라서 NUC와 미니 ITX는 임베디드 실시간 제어기(Embedded Real-time Controller)와 전문 AI 가속기(AI Accelerator) 사이에 배치되는 통합 컴퓨터(Integration Computer)로 활용하기에 적합하다.

NUC는 일반적으로 소형 패키징, 낮은 통합 복잡도(Integration Complexity), 적절한 소비전력, 빠른 소프트웨어 배포 및 일반적인 x86 연산이 핵심 요구사항일 때 적합하다. 반면 미니 ITX는 외장 가속기, 여러 PCIe 장치, 대용량 메모리, 다중 저장장치, 고급 네트워크 및 맞춤형 열설계가 필요한 경우 더욱 유리하다. 따라서 플랫폼 선정은 최초 시제품의 요구사항만이 아니라 전체 제품 수명주기에 걸친 확장 요구사항을 반영해야 한다.

엣지 PC는 인접한 컴퓨팅 계층(Compute Layer)과의 역할 관계를 고려하여 선정해야 한다. MCU와 ECU는 결정론적 모터 제어, 액추에이터(Actuator), 안전 기능(Safety Function), 저수준 입출력(Low-level I/O)을 담당하고, 젯슨급 프로세서는 특화된 임베디드 AI 워크로드를 수행할 수 있다. 이때 x86 엣지 PC는 오케스트레이션(Orchestration), 상위 인지, 매핑, 로깅, 진단, 애플리케이션 서비스 및 플릿이나 온프레미스(On-premise) 인프라와의 인터페이스를 담당할 수 있다.

피지컬 AI(Physical AI) 로봇에서는 인지 및 지능형 행동(Intelligent Behavior)이 기반 제어 전자장치보다 빠르게 발전할 수 있기 때문에 이러한 이기종 컴퓨팅 자원 분담(Heterogeneous Compute Allocation)이 더욱 중요해진다. 모듈형 미니 ITX 아키텍처는 높은 업그레이드 자유도를 제공하는 반면 NUC는 소형화와 배포 단순성에서 장점을 갖는다. 제어, AI 가속, 엣지 컴퓨팅, 네트워크 서비스 사이에 명확한 인터페이스를 유지하면 전체 전기 아키텍처를 다시 설계하지 않고도 각각의 컴퓨팅 요소를 독립적으로 발전시킬 수 있다.

최종 선정은 CPU 성능, 메모리, PCIe 확장성, 이더넷 대역폭(Ethernet Bandwidth), 저장장치 용량, 소비전력, 열적 여유(Thermal Margin), 기계적 강건성(Mechanical Robustness), 소프트웨어 호환성, 유지보수성(Maintainability), 제품 수명주기 공급성(Lifecycle Availability), 전체 통합 비용(Total Integration Cost)을 포함하는 균형 잡힌 엔지니어링 평가를 기반으로 해야 한다. 가장 적합한 플랫폼은 반드시 가장 작거나 가장 빠른 컴퓨터가 아니라, 목표 운용 수명 전체에서 충분한 환경적 여유와 확장 여유를 확보하면서 요구되는 로봇 워크로드를 안정적으로 지속 수행할 수 있는 컴퓨터이다.

## 04.02. PCIe Expansion Design

![](images/image2.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 엣지 PC(Robotics Edge PC)의 PCIe 확장 설계(PCIe Expansion Design)는 고성능 주변장치들이 프로세서가 제공하는 통신 자원을 어떻게 공유할 것인지를 결정한다. 외장 GPU(Discrete GPU), 고속 이더넷 어댑터(High-speed Ethernet Adapter), 프레임 그래버(Frame Grabber), CAN 인터페이스, NVMe 저장장치, FPGA 가속기(FPGA Accelerator), 특수 센서 데이터 수집 카드(Sensor Acquisition Card) 등이 모두 PCI 익스프레스(PCI Express)에 의존할 수 있다. 따라서 확장 아키텍처는 단순한 슬롯 집합이 아니라 시스템 수준 자원(System-level Resource)으로 계획해야 한다.

PCI 익스프레스(PCI Express)는 하나 이상의 레인(Lane)으로 구성된 점대점 직렬 링크(Point-to-point Serial Link)를 통해 동작한다. 일반적인 구성에는 x1, x2, x4, x8, x16이 있으며 세대(Generation)가 높아질수록 개별 레인의 전송 성능이 증가한다. 물리적으로 x16 커넥터를 사용한다고 해서 반드시 16개의 전기적 레인이 모두 활성화되는 것은 아니므로 메인보드 사양을 주의 깊게 확인해야 한다. 기계적 커넥터 크기, 전기적 레인 할당, PCIe 세대, 실제 프로세서 연결 구조는 서로 독립적인 설계 요소이다.

첫 번째 엔지니어링 단계는 전체 엣지 컴퓨터에 대한 PCIe 자원 맵(PCIe Resource Map)을 작성하는 것이다. 계획된 각 장치는 필요한 레인 폭(Lane Width), PCIe 세대, 예상 지속 대역폭(Sustained Bandwidth), 지연시간 민감도(Latency Sensitivity), 물리적 커넥터와 연결되어야 한다. 이후 각 인터페이스가 CPU에서 직접 제공되는지, 플랫폼 칩셋(Platform Chipset)을 통하는지, 또는 PCIe 스위치(PCIe Switch)를 경유하는지 확인해야 한다. 이러한 매핑을 통해 개별 슬롯 사양만으로는 발견하기 어려운 잠재적인 병목현상(Bottleneck)을 식별할 수 있다.

CPU 직접 연결 PCIe(CPU-direct PCIe)는 일반적으로 높은 처리량이나 예측 가능한 지연시간이 필요한 장치에 우선적으로 사용된다. 인지(Perception) 또는 AI 가속에 사용하는 외장 GPU는 x8이나 x16 연결이 필요할 수 있으며, 고속 프레임 그래버와 네트워크 어댑터도 추가적인 x4 또는 x8 자원을 사용할 수 있다. 칩셋에 연결된 장치들은 프로세서로 향하는 하나의 상위 링크(Upstream Link)를 공유할 수 있으므로, 독립적으로 보이는 여러 인터페이스가 동시에 동작할 때 동일한 총 대역폭을 두고 경쟁할 수 있다.

대역폭 계획(Bandwidth Planning)은 인터페이스의 이론적인 최대 속도만이 아니라 실제 지속 트래픽(Sustained Traffic)을 기준으로 수행해야 한다. 다중 카메라 시스템(Multi-camera System)은 영상 스트림을 지속적으로 전송하고, 3D 라이다 처리는 상당한 메모리 트래픽을 발생시킬 수 있으며, 센서 기록 과정에서는 인지 알고리즘이 동일한 데이터를 사용하는 동안 대규모 데이터가 NVMe 저장장치에 기록될 수 있다. 따라서 최악 조건의 기록, 추론(Inference), 시각화 및 네트워크 전송이 동시에 수행되는 상황에서 PCIe 사용률을 평가해야 한다.

PCIe 세대 선정(PCIe Generation Selection)은 대역폭과 구현 여유(Implementation Margin)에 모두 영향을 준다. 새로운 세대는 레인당 더 높은 대역폭을 제공하므로 과거에 더 넓은 연결이 필요했던 워크로드를 x4 인터페이스만으로 처리할 수도 있다. 그러나 신호 속도가 증가할수록 PCB 배선, 커넥터 품질, 라이저 케이블(Riser Cable), 어댑터 및 신호 손실에 더욱 민감해진다. 따라서 요구 대역폭을 더 낮은 세대에서 충분한 구현 여유와 높은 신뢰성으로 확보할 수 있다면 최신 세대가 항상 최선의 선택인 것은 아니다.

레인 분할(Lane Bifurcation)은 프로세서와 BIOS가 필요한 구성을 지원할 경우 하나의 넓은 PCIe 인터페이스를 여러 개의 작은 인터페이스로 분할할 수 있도록 한다. 예를 들어 x16 자원을 두 개의 x8 링크 또는 네 개의 x4 링크로 구성할 수 있다. 이는 여러 가속기나 NVMe 장치를 사용하는 로봇 시스템에서 유용하지만, 분할 지원 여부는 물리적 슬롯만 보고 판단해서는 안 되며 CPU, 메인보드, 펌웨어(Firmware), 커넥터, 운영체제(Operating System) 수준에서 모두 검증해야 한다.

PCIe 스위치(PCIe Switch)는 필요한 엔드포인트(Endpoint)의 수가 직접 제공되는 루트 포트(Root Port) 자원보다 많을 때 연결성을 확장할 수 있다. 여러 하위 장치가 하나의 상위 PCIe 연결을 통해 통신할 수 있으므로 아키텍처 유연성이 향상되고 모듈식 확장이 가능하다. 그러나 PCIe 스위치가 프로세서의 실제 대역폭 자체를 증가시키는 것은 아니다. 여러 하위 장치가 동시에 많은 데이터를 전송하면 전체 처리량은 상위 연결과 스위치 아키텍처의 대역폭에 의해 제한된다.

외장 GPU(Discrete GPU) 통합에서는 충분한 폭의 슬롯을 확보하는 것만으로는 부족하다. GPU의 물리적 크기, 냉각 공기 흐름(Cooling Airflow), 보조 전원 커넥터(Auxiliary Power Connector), 최대 전기 부하(Peak Electrical Load), 구조적 고정(Structural Retention), 인접 슬롯 접근성을 함께 고려해야 한다. 소형 미니 ITX(Mini-ITX) 시스템에서는 듀얼 슬롯(Dual-slot) 이상의 GPU가 논리적으로 충분한 PCIe 레인이 남아 있어도 다른 인터페이스를 물리적으로 가릴 수 있다. 따라서 전기 아키텍처와 기계적 패키징(Mechanical Packaging)을 함께 설계해야 한다.

고속 이더넷 확장(High-speed Ethernet Expansion) 역시 주요 PCIe 자원 소비 요소가 될 수 있다. 다중 포트 2.5GbE, 10GbE 또는 그 이상의 네트워크 어댑터가 카메라, 라이다, 저장장치 또는 외부 컴퓨팅 노드(External Compute Node)의 데이터를 집선할 수 있다. 필요한 PCIe 대역폭은 단일 포트의 명목 속도가 아니라 모든 활성 포트에서 동시에 발생하는 트래픽을 기준으로 산정해야 한다. 네트워크 처리 오버헤드(Network Processing Overhead), DMA 동작, 패킷 전송률(Packet Rate), 인터럽트 처리(Interrupt Handling), CPU 친화도(CPU Affinity) 역시 실제 시스템 성능에 영향을 줄 수 있다.

엣지 PC가 여러 산업용 또는 자동차용 카메라 스트림을 입력받는 경우 프레임 그래버(Frame Grabber)는 특히 중요하다. 카메라 아키텍처에 따라 PCIe 카드는 GMSL, FPD-Link, CoaXPress 등의 특수 인터페이스를 제공하고 획득한 데이터를 시스템 메모리로 직접 전달할 수 있다. 인지 파이프라인에서는 카메라 입력에서 호스트 메모리(Host Memory)를 거쳐 가속 하드웨어로 지속적인 데이터 이동이 발생하므로 프레임 그래버의 레인 할당은 GPU 및 메모리 트래픽과 함께 평가해야 한다.

NVMe 저장장치는 일반적으로 PCIe x4 연결을 사용하며 고속 센서 로깅(High-rate Sensor Logging) 과정에서 상당한 대역폭을 사용할 수 있다. 운영체제, 애플리케이션, 지도, AI 모델, 기록된 센서 데이터셋을 분리하기 위해 여러 개의 NVMe 드라이브를 사용하는 것도 유용하다. 설계자는 M.2 소켓이 전용 프로세서 레인을 사용하는지 또는 칩셋 자원을 사용하는지 확인하고, 특정 소켓 사용 시 SATA 포트가 비활성화되거나 확장 슬롯 폭이 감소하거나 다른 인터페이스의 전기적 구성이 변경되는지도 검토해야 한다.

직접 메모리 접근(Direct Memory Access, DMA)은 고처리량 로봇 컴퓨팅을 효율적으로 구현하는 핵심 기술이다. PCIe 주변장치는 CPU가 모든 데이터 블록을 직접 복사하지 않고도 데이터를 전송할 수 있어 프로세서 부하를 줄이고 파이프라인 효율을 높일 수 있다. 고급 아키텍처에서는 데이터 수집 장치, 호스트 메모리, 저장장치, 가속기 사이의 불필요한 메모리 이동을 더욱 줄일 수 있다. 실제 효과는 하드웨어, 드라이버, 운영체제 및 애플리케이션 프레임워크가 해당 데이터 전송 경로를 지원하는지에 따라 달라진다.

인터럽트 아키텍처(Interrupt Architecture) 역시 PCIe 시스템 동작에 영향을 준다. 고속 네트워크, 저장장치, 데이터 수집 장치는 드라이버와 큐(Queue)가 적절하게 구성되지 않으면 상당한 인터럽트 부하를 발생시킬 수 있다. 최신 장치는 일반적으로 MSI 또는 MSI-X를 사용하여 여러 프로세서 코어에 인터럽트 처리를 분산하지만 추가적인 시스템 튜닝이 필요할 수 있다. CPU 친화도, 수신 큐(Receive Queue), DMA 버퍼(Buffer), 실시간 태스크 배치(Real-time Task Placement)를 조정하여 주변장치 트래픽이 지연시간에 민감한 로봇 기능을 방해하지 않도록 해야 한다.

PCIe 연결이 짧은 메인보드 배선을 넘어 확장될수록 신호 무결성(Signal Integrity)의 중요성이 증가한다. 라이저 카드(Riser Card), 플렉시블 케이블(Flexible Cable), 백플레인(Backplane), 도킹 구조(Docking Structure), 맞춤형 캐리어 보드(Custom Carrier Board)는 삽입 손실(Insertion Loss), 임피던스 불연속(Impedance Discontinuity), 반사(Reflection), 추가 커넥터 문제를 발생시킨다. 고세대 PCIe 링크는 세밀한 채널 버짓(Channel Budget) 관리나 리타이머(Retimer)가 필요할 수 있으므로 불필요하게 긴 확장 경로를 피하고 실제 온도와 기계적 조건에서 전체 전기 채널을 검증해야 한다.

전원 공급(Power Delivery)은 확장 장치의 정상 상태 부하와 과도 부하(Transient Load)를 모두 고려하여 설계해야 한다. PCIe 슬롯은 표준화된 전력을 제공하지만 GPU, 가속기 및 특수 데이터 수집 카드는 추가 전원 커넥터를 요구할 수 있다. 여러 장치의 처리 상태가 동시에 변경될 때 로봇 배터리 전압 변동과 DC/DC 컨버터(DC/DC Converter)의 응답 특성도 고려해야 한다. 충분한 컨버터 용량, 배전 보호(Distribution Protection), 적절한 커넥터 정격, 접지(Grounding), 제어된 기동 순서(Startup Sequencing)를 적용하면 최대 연산 부하에서의 시스템 불안정을 방지할 수 있다.

PCIe 장치 사이의 열적 상호작용(Thermal Interaction)은 전기적 대역폭이 한계에 도달하기 전에 시스템 수준의 제한 요소가 될 수 있다. GPU, 고속 네트워크 컨트롤러, NVMe 장치, PCIe 스위치, 프레임 그래버는 모두 소형 인클로저 내부에서 열을 발생시킨다. 대형 카드 하나가 공기 흐름을 차단하면 인접 부품의 온도가 상승할 수 있다. 따라서 열설계(Thermal Design)는 모든 장치가 동시에 최악 조건의 워크로드를 수행하는 상황을 평가하고 개별 부품의 열 사양에만 의존하지 않는 충분한 냉각 여유를 확보해야 한다.

이동 로봇에서는 표준 데스크톱용 카드가 지속적인 진동과 충격을 전제로 설계되지 않았을 수 있으므로 PCIe 확장의 기계적 강건성(Mechanical Robustness)이 필수적이다. 무거운 GPU나 높이가 큰 확장 카드는 메인보드 커넥터에 상당한 기계적 하중을 가할 수 있다. 브래킷(Bracket), 카드 고정장치(Card Retainer), 지지 프레임(Support Frame), 케이블 스트레인 릴리프(Cable Strain Relief), 내진동 마운팅(Vibration-resistant Mounting)을 적용하여 메인보드 슬롯만이 확장 장치를 구조적으로 지지하지 않도록 설계해야 한다.

최종 하드웨어 아키텍처를 확정하기 전에 펌웨어 및 소프트웨어 호환성(Firmware and Software Compatibility)을 검증해야 한다. BIOS 설정은 레인 분할, PCIe 세대, 주소 공간(Address Space), 전원 관리(Power Management), 장치 인식(Device Enumeration)에 영향을 줄 수 있다. 리눅스 커널(Linux Kernel), ROS 2 통합, 제조사 드라이버, CUDA 또는 가속기 소프트웨어, 네트워크 드라이버 및 펌웨어 버전을 하나의 완전한 구성으로 검증해야 한다. 안정적인 드라이버 지원이 없는 하드웨어 호환성만으로는 양산 가능한 로봇 플랫폼(Production-ready Robotics Platform)이라고 할 수 없다.

강건한 PCIe 확장 설계는 레인 할당, 대역폭 분석, 토폴로지(Topology), 신호 무결성, 전원, 냉각, 기계적 고정, 펌웨어 및 소프트웨어를 하나의 통합 아키텍처로 결합해야 한다. 향후 추가될 센서나 가속기를 위한 확장 여유(Expansion Margin)도 확보해야 한다. 설계 목표는 가능한 최대 수의 PCIe 장치를 장착하는 것이 아니라, 로봇의 목표 수명주기 전체에서 필요한 모든 장치가 동시에 동작하면서도 예측 가능한 성능을 안정적으로 유지하도록 만드는 것이다.

## 04.03. PoE Integration

![](images/image3.png){width="7.268055555555556in" height="7.268055555555556in"}

이더넷 전원 공급(Power over Ethernet, PoE) 통합을 사용하면 로봇 엣지 PC(Robotics Edge PC)가 하나의 이더넷 케이블(Ethernet Cable)을 통해 네트워크 통신과 전력을 동시에 공급할 수 있다. 이는 산업용 카메라(Industrial Camera), IP 카메라(IP Camera), 소형 라이다(LiDAR), 무선 액세스 포인트(Wireless Access Point), 보조 임베디드 장치(Auxiliary Embedded Device)와 같이 분산 배치되는 센서에 특히 유용하다. 전력과 데이터를 하나로 통합하면 하네스 복잡성(Harness Complexity), 커넥터 수, 설치 작업량 및 로봇 내부에 필요한 별도의 DC 전원 분기 수를 줄일 수 있다.

PoE 아키텍처(PoE Architecture)는 전력 공급 장치(Power Sourcing Equipment, PSE)와 하나 이상의 수전 장치(Powered Device, PD)로 구성된다. 엣지 PC, PoE 스위치(PoE Switch), 또는 전용 PoE 네트워크 인터페이스가 일반적으로 PSE 역할을 하며 카메라와 기타 센서는 PD로 동작한다. 전력이 공급되기 전에 표준화된 감지(Detection) 및 등급 분류(Classification) 절차를 통해 PSE는 연결된 장치가 PoE를 지원하는지와 필요한 전력 수준을 확인할 수 있다.

IEEE 802.3af, 802.3at, 802.3bt는 실제 시스템에서 사용되는 주요 PoE 전력 규격(PoE Power Standard)을 나타낸다. IEEE 802.3af는 비교적 저전력 장치를 지원하고 802.3at는 고성능 카메라와 같은 장치에 더 높은 전력 예산(Power Budget)을 제공한다. IEEE 802.3bt는 네 쌍의 이더넷 선로를 모두 활용하여 전력 공급 능력을 크게 확장한다. 따라서 플랫폼 선정은 계획된 각 센서가 요구하는 PoE 규격과 최대 입력 전력을 확인하는 것부터 시작해야 한다.

전체 PoE 전력 예산(Total PoE Power Budget)은 개별 포트의 최대 정격보다 중요하다. 4포트 인터페이스가 각 커넥터에서 높은 전력을 지원하더라도 모든 포트에 최대 전력을 동시에 공급하지 못할 수 있다. 로봇 엔지니어는 모든 PD의 최악 조건 소비전력 합계를 계산하고 기동 동작, 히터(Heater) 작동, 조명(Illumination), 액추에이터 기능(Actuator Function), 환경 조건, 변환 손실(Conversion Loss), 적절한 엔지니어링 여유(Engineering Margin)를 포함해야 한다.

PoE는 카메라 아키텍처(Camera Architecture)를 크게 단순화할 수 있다. 기존 이더넷 카메라는 통신용 케이블 하나와 DC 전원을 위한 별도의 전선이 필요하여 하네스 크기와 커넥터 복잡성이 증가할 수 있다. PoE 카메라는 센서와 엣지 컴퓨터 또는 스위치 사이에서 하나의 이더넷 케이블만 사용할 수 있다. 이러한 장점은 여러 카메라가 AMR, 점검 로봇(Inspection Robot), 모바일 매니퓰레이터(Mobile Manipulator), 실외 자율주행 플랫폼(Outdoor Autonomous Platform) 주변에 분산 배치되는 경우 특히 중요하다.

그러나 PoE를 적용한다고 해서 로봇 수준의 전원 엔지니어링(Robot-level Power Engineering)이 필요 없어지는 것은 아니다. PSE는 궁극적으로 로봇 배터리에서 DC/DC 변환 및 보호 아키텍처(Protection Architecture)를 통해 에너지를 공급받는다. 배터리 전압은 충전 상태(State of Charge), 가속, 회생 동작(Regenerative Event), 충전 및 과도 부하에 따라 변화할 수 있다. 따라서 PoE 서브시스템(PoE Subsystem)은 로봇의 최악 운전 조건에서도 요구 출력을 유지할 수 있는 안정적인 전원 레일(Power Rail)로부터 공급받아야 한다.

DC/DC 컨버터(DC/DC Converter)의 용량을 산정할 때 엣지 PC와 PoE가 동일한 전원을 공유한다면 엣지 PC 부하와 전체 PoE 부하를 모두 포함해야 한다. 여러 카메라를 포함하는 시스템에서는 모든 PD가 동시에 활성화될 때 전력 요구량이 크게 증가할 수 있다. 또한 컨버터 효율(Converter Efficiency)과 열적 디레이팅(Thermal Derating)을 고려해야 하는데, 배터리에서 요구되는 입력 전력은 원격 PoE 장치에 실제로 전달되는 유효 전력보다 크기 때문이다.

기동 순서 제어(Startup Sequencing)를 적용하면 과도한 돌입 전류(Inrush Current)를 방지하고 시스템 안정성을 향상시킬 수 있다. 엣지 PC가 시작될 때 모든 PoE 센서를 즉시 활성화하는 대신 PSE 하드웨어와 소프트웨어가 지원한다면 포트를 순차적으로 활성화할 수 있다. 이를 통해 동시 기동 전력 요구량을 줄이고 핵심 센서에 우선순위를 부여할 수 있다. 제어된 기동 순서는 전체 로봇 컴퓨터를 재부팅하지 않고 개별 센서를 재시작하는 장애 복구(Fault Recovery)에도 활용할 수 있다.

포트별 전원 제어(Per-port Power Control)는 자율 로봇(Autonomous Robot)에서 유용한 기능이다. 응답하지 않는 카메라 또는 네트워크 센서는 경우에 따라 PoE 전원을 비활성화한 후 다시 활성화하여 복구할 수 있다. 네트워크 컨트롤러(Network Controller)나 관리형 PoE 스위치(Managed PoE Switch)가 이를 지원하면 소프트웨어가 장치 상태를 감시하고 선택적인 전원 재인가(Power Cycling)를 수행할 수 있다. 이는 애플리케이션 재시작, 드라이버 재로딩 또는 전체 시스템 재부팅 이외의 추가적인 복구 수단을 제공한다.

네트워크 대역폭(Network Bandwidth)은 PoE 전력 예산과 독립적으로 평가해야 한다. 충분한 전력을 공급할 수 있다고 해서 충분한 통신 성능이 보장되는 것은 아니다. 여러 고해상도 카메라(High-resolution Camera)는 각 PoE 포트가 전기적 정격 범위 내에 있더라도 지속적인 이더넷 트래픽으로 인해 1GbE 업링크(Uplink)의 용량을 초과할 수 있다. 따라서 아키텍처에서는 전체 센서 데이터 전송률과 전체 소비전력을 서로 독립된 설계 요소로 계산해야 한다.

다중 카메라 엣지 PC(Multi-camera Edge PC)는 여러 개의 독립적인 이더넷 인터페이스 또는 고속 업링크를 통해 연결된 PoE 스위치를 사용할 수 있다. 예를 들어 센서 측의 기가비트 이더넷(Gigabit Ethernet) 연결을 엣지 컴퓨터 방향의 2.5GbE, 5GbE 또는 10GbE 연결로 집선할 수 있다. 적절한 토폴로지(Topology)는 카메라 해상도, 프레임 속도(Frame Rate), 압축(Compression), 동기화(Synchronization), 기록 요구사항, 원시 데이터(Raw Data) 또는 처리된 데이터가 네트워크를 지속적으로 통과해야 하는지에 따라 결정된다.

PCIe PoE 네트워크 카드(PCIe PoE Network Card)는 여러 개의 전원 공급 이더넷 포트를 미니 ITX(Mini-ITX) 또는 산업용 엣지 PC(Industrial Edge PC)에 직접 통합하는 소형 솔루션을 제공한다. 이러한 카드는 이더넷 통신과 PSE 기능을 결합하지만 PCIe 레인, 전력, 냉각 및 기계적 요구사항이 추가된다. 따라서 전체 확장 아키텍처에서 GPU, 프레임 그래버(Frame Grabber), NVMe 저장장치 및 기타 PCIe 장치와 함께 총 네트워크 대역폭과 PoE 출력을 평가해야 한다.

외부 관리형 PoE 스위치(External Managed PoE Switch)는 또 다른 통합 전략을 제공한다. 센서 네트워크를 엣지 PC 메인보드로부터 분리할 수 있으며 더 많은 포트, 독립적인 전원 관리(Power Management), 진단(Diagnostics), VLAN 구성 및 간편한 교체 기능을 제공할 수 있다. 반면 추가적인 인클로저 공간, 전력 변환, 케이블링, 열 방출이 필요하며 로봇 환경에서 기계적으로 고정하고 검증해야 하는 또 하나의 전자 모듈이 추가된다는 절충점(Tradeoff)이 존재한다.

PoE 센서가 전용 인지 네트워크(Perception Network)를 구성하는 경우 네트워크 분할(Network Segmentation)을 통해 신뢰성과 보안성을 향상시킬 수 있다. 카메라와 라이다 장치를 별도의 물리적 인터페이스나 VLAN을 이용하여 플릿 통신(Fleet Communication), 유지보수 접근(Maintenance Access), 클라우드 연결(Cloud Connectivity), 기타 외부 네트워크와 분리할 수 있다. 이를 통해 관련 없는 트래픽이 인지 데이터와 직접 경쟁하는 것을 방지하고 진단, 사이버보안 정책(Cybersecurity Policy), 장애 격리(Fault Containment)를 위한 명확한 경계를 제공할 수 있다.

케이블 선정(Cable Selection)은 데이터 무결성(Data Integrity)과 전력 공급 모두에 영향을 준다. 이더넷 도체는 고속 차동 신호(High-speed Differential Signal)를 전송하면서 동시에 전류를 전달하므로 도체 저항, 케이블 길이, 온도, 번들링(Bundling), 차폐(Shielding), 커넥터 품질이 시스템 성능에 영향을 미친다. 과도한 저항은 전압 강하(Voltage Drop)와 케이블 발열을 증가시킨다. 여러 PoE 케이블이 제한된 공간을 통해 함께 배선되는 소형 로봇 하네스에서는 이러한 열적 영향이 더욱 커질 수 있다.

차폐 이더넷(Shielded Ethernet)은 전기적으로 노이즈가 많은 로봇 플랫폼에서 전자파 적합성(Electromagnetic Compatibility, EMC)을 향상시킬 수 있지만 차폐는 명확하게 설계된 접지 전략(Grounding Strategy)과 함께 적용해야 한다. 모터, 인버터(Inverter), DC/DC 컨버터, 스위칭 전원공급장치(Switching Power Supply), 고전류 배터리 배선은 상당한 전자기 간섭(Electromagnetic Interference, EMI)을 발생시킬 수 있다. 케이블은 노이즈가 큰 전력 회로와 적절한 거리를 유지하고 차폐 종단(Shield Termination)과 섀시 본딩(Chassis Bonding)은 의도하지 않은 접지 전류 경로가 발생하지 않도록 설계해야 한다.

표준 RJ45 커넥터는 주로 고정형 네트워크 환경을 위해 개발되었기 때문에 커넥터 강건성(Connector Robustness)에 특별한 주의가 필요하다. 지속적인 진동, 충격, 인장력, 습기 및 반복적인 정비 작업은 이동 로봇에서 연결 신뢰성을 저하시킬 수 있다. 환경 및 유지보수 요구사항에 따라 산업용 잠금식 이더넷 커넥터(Industrial Locking Ethernet Connector), 러기드 RJ45(Ruggedized RJ45), M12 이더넷 커넥터(M12 Ethernet Connector), 또는 보호된 내부 장착 방식을 적용하는 것이 더 적합할 수 있다.

열설계(Thermal Design)에는 PSE 전자회로에서 발생하는 손실도 포함해야 한다. 외부 장치에 수십 또는 수백 와트의 전력을 공급하려면 스위칭 및 전력 관리 부품이 필요하며, 이들은 엣지 PC 또는 PoE 스위치 내부에서 열을 발생시킨다. 따라서 CPU와 GPU가 허용 온도 범위에 있더라도 PoE 회로가 자체 열 한계에 도달할 수 있다. 최악 조건 분석에는 최대 센서 전력, 높은 주변 온도 및 감소된 공기 흐름을 함께 고려해야 한다.

장애 보호(Fault Protection)는 손상된 케이블이나 센서 하나가 전체 인지 시스템을 정지시키지 않도록 설계해야 한다. 개별 포트 전류 제한(Current Limiting), 단락 보호(Short-circuit Protection), 과전압 보호(Overvoltage Protection), 과열 차단(Thermal Shutdown), 장애 보고(Fault Reporting)를 통해 비정상 장치를 격리할 수 있다. 임무 요구사항에 따라 핵심 카메라를 서로 다른 PoE 컨트롤러나 전원 도메인(Power Domain)에 분산하여 하나의 PSE 고장이 모든 시각 인지 기능을 동시에 제거하지 않도록 구성할 수도 있다.

소프트웨어 모니터링(Software Monitoring)을 적용하면 PoE를 단순한 전력 공급 방식에서 로봇 진단 아키텍처(Robot Diagnostic Architecture)의 일부로 확장할 수 있다. 시스템은 포트 상태, 협상된 전력 등급(Negotiated Power Class), 소비전류, 링크 상태(Link Status), 패킷 통계(Packet Statistics), 센서 가용성(Sensor Availability), 복구 시도 등을 기록할 수 있다. 이러한 측정값을 ROS 2 진단 및 플릿 텔레메트리(Fleet Telemetry)와 연계하면 유지보수 담당자가 센서 고장, 케이블 장애, 네트워크 혼잡 및 전원 관련 문제를 구분하는 데 도움이 된다.

따라서 PoE 통합은 이더넷 토폴로지(Ethernet Topology), PCIe 확장, 엣지 PC 전원공급장치, 열 관리(Thermal Management), 하네스 배선(Harness Routing), 접지, 진단 및 기계적 패키징과 동시에 설계해야 한다. PoE의 핵심 가치는 단순히 전원 케이블 하나를 제거하는 것에 있지 않다. 적절하게 설계된 PoE는 통신, 전력 분배(Power Distribution), 모니터링, 격리(Isolation), 복구 기능을 하나의 통합된 서브시스템으로 관리할 수 있는 모듈형 센서 인터페이스(Modular Sensor Interface)를 제공한다.

양산 로봇 플랫폼(Production Robotics Platform)에서 적합한 PoE 솔루션은 최악 운전 조건에서도 필요한 모든 센서에 전력을 공급하면서 네트워크 대역폭, 전기적 여유(Electrical Margin), 열적 여유(Thermal Margin), 장애 격리 능력을 유지할 수 있는 아키텍처이다. 향후 추가될 카메라와 센서를 위한 충분한 확장 여유도 확보해야 한다. 이를 통해 전체 컴퓨팅 아키텍처 내의 엣지 PC와 인지 네트워크가 발전하더라도 로봇의 배선 및 전력 분배 시스템 전체를 다시 설계하지 않고 확장할 수 있다.

## 04.04. Edge PC Power Supply

![](images/image4.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 플랫폼(Robotics Platform)의 엣지 PC 전원공급장치(Edge PC Power Supply)는 로봇의 가변적인 배터리 에너지를 프로세서, 메모리, 저장장치, 네트워크 인터페이스, PCIe 장치 및 보조 주변장치에 필요한 안정적인 전원 레일(Power Rail)로 변환해야 한다. 안정화된 AC 전원에 연결되는 고정형 데스크톱 컴퓨터와 달리 이동 로봇은 배터리 방전, 충전, 모터 과도현상(Motor Transient), 회생 동작(Regenerative Event), 커넥터 교란 및 급격한 운전 상태 변화를 경험한다. 따라서 전원 아키텍처(Power Architecture)는 컴퓨팅 시스템 자체의 일부로 설계해야 한다.

전원 설계(Power Design)는 로봇의 배터리 아키텍처(Battery Architecture)와 엣지 PC가 허용하는 입력 전압 범위(Input Voltage Range)를 정의하는 것에서 시작한다. 공칭 24 V 또는 48 V 배터리는 운전 중 항상 정확히 해당 전압을 유지하지 않는다. 단자 전압은 충전 상태(State of Charge), 배터리 화학계(Battery Chemistry), 부하 전류, 온도, 충전 조건 및 과도 응답에 따라 변화한다. 따라서 DC/DC 변환단(DC/DC Conversion Stage)은 공칭 전압만이 아니라 예상되는 전체 배터리 전압 범위에서 안정화된 출력을 유지해야 한다.

전력 예산(Power Budgeting)은 실제로 동시에 발생할 수 있는 워크로드(Workload)를 반영해야 한다. CPU 처리, GPU 가속, NVMe 기록, PCIe 통신, 이더넷 트래픽, USB 주변장치, 냉각 팬 및 PoE 센서가 동시에 활성화될 수 있다. 설계에서는 평균 소비전력(Average Consumption), 지속 최대전력(Sustained Maximum Power), 단시간 피크 전력(Peak Power)을 구분해야 한다. 일반적인 CPU 소비전력만을 기준으로 컨버터 용량을 결정하면 여러 고성능 서브시스템이 동시에 최대 운전 상태에 진입할 때 전력이 부족해질 수 있다.

컴퓨팅 구성은 로봇의 수명주기(Lifecycle) 동안 발전할 수 있기 때문에 엔지니어링 여유(Engineering Margin)가 필요하다. 추가 메모리, 저장장치, 네트워크 어댑터, 센서 또는 가속기가 최초 설계 이후 추가되면서 소비전력이 증가할 수 있다. 또한 최대 정격에 가까운 상태로 지속적으로 운전되는 전원공급장치는 높은 온도와 과도 부하에 대한 허용 여유가 제한된다. 적절한 예비 용량(Reserve Capacity)은 신뢰성을 향상시키고 향후 업그레이드로 인해 전체 전원 서브시스템을 다시 설계해야 할 가능성을 줄인다.

DC/DC 컨버터 토폴로지(DC/DC Converter Topology)는 배터리 전압과 엣지 PC 입력 요구전압의 관계에 따라 결정된다. 전원 전압이 항상 필요한 출력전압보다 높다면 벅 컨버터(Buck Converter)가 적합하고, 전압을 높여야 한다면 부스트 컨버터(Boost Converter)를 사용할 수 있다. 배터리 전압 범위가 목표 전압보다 높거나 낮아질 수 있다면 벅-부스트 아키텍처(Buck-boost Architecture)를 통해 안정된 출력을 유지할 수 있다. 효율, 과도 응답(Transient Response), 절연(Isolation), 열 성능 및 전자파 적합성(Electromagnetic Compatibility)을 함께 평가해야 한다.

인텔 NUC급 컴퓨터(Intel NUC-class Computer)는 비교적 넓은 외부 DC 입력 범위를 지원할 수 있는 반면, 미니 ITX(Mini-ITX) 아키텍처는 ATX 방식의 내부 전원 레일 또는 전용 DC-ATX 컨버터(DC-ATX Converter)를 필요로 할 수 있다. 따라서 미니 ITX 통합에서는 안정화된 입력전원으로부터 12 V, 5 V, 3.3 V와 같은 메인보드 전원 레일을 생성하는 구성이 필요할 수 있다. 정확한 전원 아키텍처는 기존 데스크톱 전원 구성이 이동 로봇에 적합하다고 가정하지 말고 메인보드와 주변장치의 실제 요구사항에 따라 결정해야 한다.

PCIe 확장(PCIe Expansion)은 전원 아키텍처를 크게 변화시킬 수 있다. 외장 GPU(Discrete GPU), 고속 네트워크 카드, 프레임 그래버(Frame Grabber), FPGA 가속기(FPGA Accelerator), 추가 NVMe 저장장치는 지속 부하와 과도 부하를 모두 증가시킬 수 있다. 일부 장치는 PCIe 커넥터에서 모든 전력을 공급받지만 다른 장치는 별도의 보조 전원 연결(Auxiliary Power Connection)을 필요로 한다. 따라서 엣지 PC 전원공급장치는 실제 장착되는 전체 하드웨어 구성을 기준으로 용량을 결정하고 목표 제품 수명주기 동안 예상되는 확장까지 반영해야 한다.

PoE 통합(PoE Integration)은 엣지 컴퓨터 또는 연결된 PoE 스위치(PoE Switch)가 분산된 카메라와 센서에 전력을 공급할 수 있기 때문에 또 하나의 주요 부하가 된다. PoE 서브시스템에 필요한 입력전력은 모든 수전 장치(Powered Device)의 소비전력뿐만 아니라 변환 손실과 케이블 손실까지 포함한다. 엣지 컴퓨팅과 PoE가 하나의 DC/DC 컨버터를 공유한다면 센서 활성화가 컴퓨터 전원을 불안정하게 만들지 않도록 두 시스템의 최악 조건 부하를 합산해야 한다.

이동 로봇에서는 과도 응답(Transient Behavior)이 특히 중요하다. 모터, 조향 액추에이터(Steering Actuator), 펌프, 매니퓰레이터(Manipulator), 컨택터(Contactor) 및 기타 고전류 부하는 배터리 전압을 급격하게 변화시킬 수 있다. 회생 제동(Regenerative Braking)이나 유도성 스위칭(Inductive Switching)은 전기 아키텍처에 따라 역극성 또는 과전압 교란을 발생시킬 수 있다. 입력 필터링(Input Filtering), 과도전압 억제(Transient Suppression), 충분한 커패시턴스(Capacitance), 적절하게 선정된 보호 부품을 적용하여 이러한 교란이 민감한 컴퓨팅 전자장치로 전달되는 것을 방지해야 한다.

저전압 동작(Undervoltage Behavior)은 의도적으로 정의되어야 한다. 배터리 전압이 컨버터의 안정적인 동작 범위 아래로 떨어졌을 때 엣지 PC가 반복적으로 리셋되도록 방치하면 저장장치가 손상되거나 예측하기 어려운 로봇 동작이 발생할 수 있다. 전원 컨트롤러(Power Controller)는 저전압 상태에 접근하는 것을 감지하고 제어된 대응을 수행해야 한다. 시스템 요구사항에 따라 컴퓨팅 부하 감소, 비핵심 주변장치 비활성화, 상위 감독 소프트웨어(Supervisory Software) 통보 또는 운영체제의 정상 종료(Orderly Shutdown)를 수행할 수 있다.

과전압 보호(Overvoltage Protection)는 충전 장애, 회생 동작, 배선 오류 및 과도 교란에 대한 보완적인 보호 수단을 제공한다. 보호 회로에는 과도전압 억제기(Transient-voltage Suppressor), 서지 억제(Surge Suppression), 입력 클램프(Input Clamp), 제어형 차단 장치(Controlled Disconnect Device) 등이 포함될 수 있다. 보호 임계값은 정상적인 운전 전압보다 높으면서도 하위 전자장치가 손상될 수 있는 수준보다 낮아야 한다. 배터리 보호, PDU 보호, DC/DC 변환 및 엣지 PC 입력 보호를 상호 조정하여 불필요한 중복 보호나 보호 공백이 발생하지 않도록 해야 한다.

역극성 보호(Reverse-polarity Protection)는 제조, 유지보수 및 현장 정비 과정에서 잘못된 연결로 인해 민감한 전자장치가 즉시 손상되는 것을 방지하는 데 유용하다. MOSFET 기반 보호(MOSFET-based Protection)는 고전류 시스템에서 일반적인 직렬 다이오드보다 낮은 손실을 제공할 수 있다. 또한 입력 퓨즈(Input Fuse) 또는 전자식 회로 보호(Electronic Circuit Protection)를 적용하여 고장난 엣지 PC나 컨버터를 로봇의 나머지 전원 네트워크로부터 격리하고 상위 보호 장치와 보호 협조(Protection Coordination)를 이루도록 해야 한다.

엣지 PC는 상당한 입력 커패시턴스(Input Capacitance)를 포함할 수 있으므로 돌입 전류(Inrush Current)를 고려해야 한다. 전원이 처음 연결될 때 이러한 커패시터가 충전되면서 짧은 시간 동안 높은 전류가 발생하여 커넥터, 릴레이, DC/DC 컨버터 또는 배터리 보호회로에 부담을 줄 수 있다. 소프트 스타트(Soft-start), 프리차지(Pre-charge), 전류 제한(Current Limiting), 단계적 전원 시퀀싱(Staged Power Sequencing)을 적용하여 이러한 영향을 줄일 수 있다. 적절한 방식은 시스템 커패시턴스, 전원 임피던스(Source Impedance), 스위칭 장치 및 허용 가능한 기동 시간에 따라 결정된다.

기동 순서 제어(Startup Sequencing)는 컴퓨팅 장치와 주변장치가 어떤 순서로 동작을 시작할지를 결정한다. 엣지 PC를 카메라, PoE 장치, 저장장치 모듈 또는 외부 가속기보다 먼저 기동하여 운영체제와 모니터링 서비스를 우선 초기화할 수 있다. 이후 핵심 위치추정(Localization) 및 안전 관련 지원 장치에 비핵심 주변장치보다 높은 우선순위를 부여할 수 있다. 제어된 시퀀싱은 최대 기동 전력 요구량을 감소시키고 진단 및 검증을 위한 반복 가능한 시스템 초기화 과정을 제공한다.

리눅스 기반 엣지 PC(Linux-based Edge PC)의 전원을 갑자기 차단하면 파일시스템 작업, 데이터베이스 트랜잭션(Database Transaction), 지도 업데이트, 센서 로그 또는 AI 모델 파일이 중단될 수 있기 때문에 종료 관리(Shutdown Management)도 중요하다. 전원 관리 컨트롤러(Power-management Controller)는 점화 해제(Ignition-off) 또는 종료 요청을 감지하고 운영체제가 애플리케이션을 종료하고 저장장치를 동기화할 수 있도록 충분한 유지 시간을 제공할 수 있다. 소프트웨어가 종료 완료를 확인하거나 정의된 제한 시간이 경과한 후에만 주 컴퓨팅 전원 레일을 차단해야 한다.

홀드업 에너지(Hold-up Energy)는 필요한 종료 시간에 따라 입력 커패시턴스, 전용 백업 전원(Backup Supply), 또는 소형 무정전 전원공급장치(Uninterruptible Power Supply, UPS) 아키텍처를 통해 제공할 수 있다. 일반적인 목적은 배터리 전원이 상실된 이후 로봇 컴퓨터를 장시간 운전하는 것이 아니라 안전한 데이터 처리와 제어된 종료에 필요한 시간을 확보하는 것이다. 필요한 에너지는 엣지 PC 소비전력, 종료 시간, 컨버터 효율 및 안정적인 동작을 유지할 수 있는 최소 전압을 기준으로 계산해야 한다.

점화 제어(Ignition Control)는 물리적인 배터리 연결과 논리적인 컴퓨터 동작을 분리한다. 저전력 컨트롤러(Low-power Controller)는 주 엣지 PC가 꺼져 있는 동안에도 활성 상태를 유지하면서 점화 또는 로봇 상태 신호를 감시하고 필요할 때 고전력 컴퓨팅 전원을 제어할 수 있다. 이러한 아키텍처는 전체 컴퓨터를 계속 켜 두어 높은 대기전력을 소비하지 않고도 지연 종료(Delayed Shutdown), 예약 기동(Scheduled Wake-up), 원격 유지보수(Remote Maintenance), 복구 기능을 구현할 수 있게 한다.

DC/DC 컨버터의 출력 능력은 일반적으로 온도가 상승하면 감소하기 때문에 열설계(Thermal Design)와 전기적 용량 산정(Electrical Sizing)은 밀접하게 연결되어 있다. 실험실 조건에서 충분한 전력을 제공하는 컨버터도 밀폐된 로봇 인클로저에서는 디레이팅(Derating)이 필요할 수 있다. 효율 손실은 전력전자장치에서 제거해야 하는 열로 변환된다. 따라서 컨버터 위치, 방열판(Heat Sink), 공기 흐름(Airflow), 인클로저 열전도(Enclosure Conduction), 주변 온도 및 인접한 GPU나 CPU의 열원을 전원 설계에 포함해야 한다.

전자파 적합성(Electromagnetic Compatibility, EMC) 역시 시스템 수준의 요구사항이다. 스위칭 컨버터(Switching Converter)는 카메라, 이더넷, GNSS, IMU, 라이다, 오디오 시스템 및 기타 민감한 전자장치에 영향을 미치는 전도성 및 방사성 노이즈(Conducted and Radiated Noise)를 발생시킬 수 있다. 입력 및 출력 필터링, 짧은 고전류 루프, 적절한 접지(Grounding), 차폐(Shielding), PCB 레이아웃, 케이블 배선 및 센서 배선과의 분리를 통해 간섭을 제어해야 한다. 전원 무결성(Power Integrity)과 EMC는 실제 컴퓨팅 및 모터 운전 조건에서 검증해야 한다.

전원 모니터링(Power Monitoring)은 진단 및 수명주기 관리(Lifecycle Management) 능력을 향상시킨다. 입력 전압, 전류, 컨버터 온도, 출력 상태 및 누적 에너지 소비량을 측정하면 시스템이 완전히 고장나기 전에 비정상 상태를 식별할 수 있다. 이러한 값을 ROS 2 진단(ROS 2 Diagnostics) 및 플릿 텔레메트리(Fleet Telemetry)와 통합하면 엔지니어가 컴퓨팅 리셋, 열적 이벤트(Thermal Event), 센서 고장 또는 성능 저하를 로봇에서 기록된 실제 전기적 상태와 연관하여 분석할 수 있다.

강건한 엣지 PC 전원공급장치(Robust Edge PC Power Supply)는 전력 변환, 보호, 시퀀싱, 모니터링, 열 관리, EMC, 제어된 기동 및 안전한 종료를 하나의 통합된 서브시스템으로 구성해야 한다. 설계 목표는 단순히 컴퓨터가 요구하는 공칭 전압을 제공하는 것이 아니다. 배터리 전압 변화, 과도 부하, 주변장치 확장, 환경적 스트레스 및 비정상적인 전기 이벤트가 발생하더라도 로봇의 전체 운용 수명 동안 안정적인 컴퓨팅 동작을 유지해야 한다.

최종 아키텍처는 충분한 지속 전력(Continuous Power), 과도 부하 대응 능력(Transient Capability), 변환 효율(Conversion Efficiency), 열적 여유(Thermal Margin), 향후 확장 여유(Future Expansion Reserve)를 확보하면서 배터리, 전력 분배 장치(Power Distribution Unit, PDU), PoE 서브시스템, PCIe 장치 및 전체 컴퓨팅 아키텍처와 상호 조정되어야 한다. 적절하게 설계된 전원공급장치는 엣지 PC를 단순히 로봇 배터리에 연결된 소비자용 컴퓨터가 아니라 신뢰할 수 있는 컴퓨팅 노드(Dependable Computing Node)로 동작하게 하며, 안정적인 인지(Perception), 매핑(Mapping), 진단(Diagnostics), 피지컬 AI(Physical AI) 워크로드 수행에 필요한 전기적 기반을 제공한다.

## 04.05. Vibration SSD Design

![](images/image5.png){width="7.268055555555556in" height="7.268055555555556in"}

로봇 엣지 PC(Robotics Edge PC)를 위한 내진동 SSD 설계(Vibration-resistant SSD Design)는 로봇이 이동하는 동안 저장장치가 전기적, 기계적, 논리적으로 안정적인 신뢰성을 유지하도록 해야 한다. 고정형 컴퓨터와 달리 이동 로봇은 지속적인 진동(Vibration), 반복적인 충격(Shock), 가속, 바퀴 충격, 구조 공진(Structural Resonance), 온도 변화를 경험한다. 솔리드 스테이트 드라이브(Solid-state Drive, SSD)는 회전 디스크를 사용하지 않지만 커넥터, 납땜 접합부(Solder Joint), PCB 조립체, 장착 구조 및 NAND 소자는 여전히 이동 환경에 적합한 세밀한 엔지니어링을 필요로 한다.

첫 번째 설계 결정은 SSD 폼팩터(Form Factor)이다. M.2 NVMe 장치는 소형 패키징, 높은 대역폭, 직접적인 PCIe 연결을 제공하므로 NUC, 미니 ITX(Mini-ITX), 산업용 엣지 컴퓨터(Industrial Edge Computer)에 적합하다. 그러나 길고 얇은 M.2 PCB는 진동 환경에서 굽힘과 커넥터 응력을 받을 수 있다. 따라서 기계적으로 강건한 설계에서는 저장장치 성능뿐만 아니라 보드 크기, 장착 지점, 고정 방식(Retention Method), 질량 분포 및 주변 기계 구조를 함께 고려해야 한다.

M.2 모듈은 일반적으로 엣지 커넥터(Edge Connector)에 삽입되고 반대쪽 끝을 작은 나사 또는 고정 장치로 체결한다. 진동하는 로봇에서는 모듈이 충분히 지지되지 않거나 적절하게 체결되지 않은 경우 이러한 장착 구조가 기계적 취약점이 될 수 있다. 견고한 체결, 적절한 스탠드오프(Standoff), 제어된 나사 체결 토크(Screw Torque), 잠금 장치 및 추가적인 지지 구조를 적용하면 장시간 운전 중 SSD, 메인보드, 커넥터 사이의 상대적인 움직임을 줄일 수 있다.

주요 진동 방향에 대한 SSD의 장착 방향(Orientation)은 기계적 하중에 영향을 줄 수 있다. PCB를 반복적으로 굽히는 방향으로 진동이 전달되는 위치에 설치된 모듈은 기계적으로 유리한 축과 정렬된 모듈보다 더 큰 응력을 받을 수 있다. 엣지 PC 섀시, 메인보드 위치, 휠 서스펜션(Wheel Suspension), 모터 장착부 및 로봇 프레임은 모두 전달되는 진동에 영향을 준다. 따라서 저장장치 위치는 독립적인 메인보드 부품이 아니라 전체 구조 진동 전달 경로(Structural Vibration Path)의 일부로 평가해야 한다.

진동 절연(Vibration Isolation)은 로봇 섀시에서 엣지 컴퓨터로 전달되는 기계적 에너지를 감소시킬 수 있다. 엘라스토머 마운트(Elastomer Mount), 진동 감쇠 구조(Vibration-damping Structure), 절연 그로밋(Isolation Grommet), 또는 서스펜디드 트레이(Suspended Tray)를 컴퓨팅 인클로저와 로봇 프레임 사이에 적용할 수 있다. 그러나 지나치게 부드러운 마운트는 큰 변위를 발생시키거나 주요 가진 주파수(Excitation Frequency) 부근에서 공진을 형성할 수 있으므로 신중하게 설계해야 한다. 목표는 단순히 기계적 유연성을 최대화하는 것이 아니라 제어된 진동 감쇠(Controlled Attenuation)를 구현하는 것이다.

충격 하중(Shock Loading)은 지속적인 진동과 다른 조건을 나타낸다. 실외 AMR과 점검 로봇(Inspection Robot)은 연석, 이음부, 포트홀(Pothole), 장애물, 경사로 또는 우발적인 충돌을 만나 짧은 시간 동안 높은 가속도를 경험할 수 있다. SSD의 NAND 자체가 높은 충격 수준을 견딜 수 있더라도 메인보드, 커넥터, 고정 나사, 방열판(Heat Sink), 주변 구조 역시 동일한 충격을 견뎌야 한다. 따라서 시스템 검증(System Qualification)은 SSD 부품의 사양에만 의존하지 않고 조립된 전체 컴퓨팅 유닛을 대상으로 수행해야 한다.

산업용 SSD(Industrial-grade SSD)를 선정하면 가혹한 환경에서 지속적으로 운전되는 로봇에 여러 장점을 제공할 수 있다. 이러한 장치는 더 넓은 동작 온도 범위(Operating Temperature Range), 관리된 부품 공급(Component Sourcing), 향상된 내구성(Endurance), 전원 손실 보호(Power-loss Protection), 상태 모니터링(Health Monitoring), 장기간의 제품 공급성(Product Availability)을 제공할 수 있다. 로봇 저장장치는 지속적인 로깅, 지도 접근, 소프트웨어 실행, 데이터베이스 작업 및 반복적인 현장 데이터 수집을 수행하기 때문에 이러한 특성이 최대 벤치마크 성능보다 더 중요할 수 있다.

낸드 플래시(NAND Flash) 기술은 내구성, 성능, 용량 및 비용에 영향을 준다. 운영체제와 애플리케이션을 주로 저장하는 장치는 카메라, 라이다 또는 진단 데이터를 지속적으로 기록하는 저장장치와 서로 다른 쓰기 특성(Write Profile)을 갖는다. 고속 센서 기록은 로봇의 전체 수명주기 동안 SSD의 쓰기 내구성을 상당 부분 소모할 수 있다. 따라서 SSD 선정에서는 총 기록 바이트(Total Bytes Written), 일일 드라이브 쓰기량(Drive Writes Per Day), 예상 운용 기간 및 실제 현장 기록 동작을 고려해야 한다.

시스템 드라이브(System Drive)와 데이터 로깅 드라이브(Data-logging Drive)를 분리하면 신뢰성과 유지보수성을 모두 향상시킬 수 있다. 운영체제, ROS 2 소프트웨어, 구성 파일, 지도 및 AI 모델은 하나의 SSD에 저장하고 대용량 센서 데이터는 다른 SSD에 기록할 수 있다. 이를 통해 지속적인 로깅이 시스템 드라이브의 내구성을 소모하는 것을 방지하고 입출력 경합(I/O Contention)을 줄일 수 있다. 또한 로깅 드라이브가 고장나거나 수명이 다해도 전체 로봇 소프트웨어 환경을 다시 구축하지 않고 교체할 수 있다.

NVMe의 열적 특성(Thermal Behavior)은 진동 설계와 함께 고려해야 한다. 고성능 SSD 컨트롤러는 지속적인 쓰기 작업 중 상당한 열을 발생시킬 수 있으며 여러 카메라 또는 고속 센서 스트림을 기록할 때 특히 문제가 될 수 있다. 열 스로틀링(Thermal Throttling)은 저장장치 처리량을 급격히 감소시키고 로깅 큐(Logging Queue)를 누적시킬 수 있다. 히트 스프레더(Heat Spreader) 또는 방열판은 지속 성능을 향상시킬 수 있지만 추가된 질량이 M.2 커넥터나 SSD PCB에 과도한 진동 하중을 전달하지 않도록 기계적으로 지지해야 한다.

열 인터페이스 재료(Thermal Interface Material)는 진동, 제조 공차(Manufacturing Tolerance), 반복적인 온도 사이클(Temperature Cycle)에서도 안정적인 접촉을 유지해야 한다. 열 패드(Thermal Pad)를 사용하여 SSD 컨트롤러 또는 모듈을 히트 스프레더, 메인보드 실드 또는 섀시 표면과 연결할 수 있다. 열 패드의 압축량은 SSD를 휘게 하지 않으면서 효과적인 열전도를 제공하도록 제어해야 한다. 따라서 저장장치 아키텍처가 완성된 이후 무거운 방열판을 별도로 추가하는 방식이 아니라 기계 설계와 열설계를 동시에 조정해야 한다.

2.5인치 SATA 또는 외부 장착 저장장치처럼 케이블 기반 저장장치(Cable-based Storage)를 사용하는 경우에는 추가적인 고려가 필요하다. SATA 데이터 및 전원 커넥터는 확실한 고정 구조가 없으면 반복적인 진동으로 느슨해질 수 있다. 잠금식 커넥터(Locking Connector), 짧은 케이블, 스트레인 릴리프(Strain Relief), 제어된 배선 및 기계적으로 고정된 드라이브를 적용하면 신뢰성을 향상시킬 수 있다. 특히 하네스가 섀시 움직임이나 정비 작업의 영향을 받는 위치에서는 케이블 질량이 SSD 커넥터를 지속적으로 당기지 않도록 해야 한다.

NVMe는 별도의 데이터 케이블을 제거하지만 신뢰성 문제의 중심을 메인보드 커넥터와 PCIe 인터페이스로 이동시킨다. 고속 PCIe 신호는 안정적인 전기 접촉과 우수한 신호 무결성(Signal Integrity)을 요구한다. 간헐적인 커넥터 움직임은 링크 오류(Link Error), 링크 재훈련(Link Retraining), 링크 폭 감소 또는 장치 인식 상실(Device Disappearance)을 발생시킬 수 있다. 따라서 기계적 고정은 통신 신뢰성에 직접적으로 기여하며 저장장치 진단에는 파일시스템 접근 가능 여부뿐만 아니라 PCIe 오류 모니터링도 포함해야 한다.

진동으로 인한 커넥터 교란과 로봇 수준의 전기적 과도현상 모두 SSD 동작을 중단시킬 수 있기 때문에 전원 무결성(Power Integrity)이 중요하다. 메타데이터 업데이트, 데이터베이스 트랜잭션(Database Transaction), 파일시스템 쓰기 도중 예상하지 못한 전원 손실이 발생하면 SSD가 기계적으로 손상되지 않았더라도 데이터 손상이 발생할 수 있다. 따라서 안정적인 DC/DC 변환, 충분한 로컬 커패시턴스(Local Capacitance), 제어된 종료(Controlled Shutdown), 적절한 전원 손실 보호를 기계적 진동 설계와 함께 적용해야 한다.

전원 손실 보호(Power-loss Protection)는 중요한 로그, 지도, 구성 데이터베이스 또는 트랜잭션 정보를 저장하는 장치에서 특히 유용하다. 엔터프라이즈 또는 산업용 SSD(Enterprise or Industrial SSD)는 입력 전원이 사라질 때 휘발성 매핑 정보(Volatile Mapping Information)를 안전하게 기록할 수 있도록 내부 에너지 저장장치를 포함할 수 있다. 이는 정상적인 운영체제 종료(Orderly Operating-system Shutdown)를 대체하지 않지만 배터리 분리, PDU 고장, 케이블 장애 또는 비상 전기 이벤트로 갑자기 전원이 제거되는 경우 추가적인 보호 계층을 제공한다.

파일시스템 및 소프트웨어 아키텍처(Filesystem and Software Architecture) 역시 저장장치의 복원력(Storage Resilience)에 영향을 준다. 불필요하게 빈번한 쓰기는 최소화하고 적절한 경우 임시 데이터를 메모리에 저장할 수 있으며 로깅 정책에는 파일 순환(File Rotation)과 용량 제한을 포함해야 한다. 핵심 구성 데이터는 원자적 쓰기(Atomic Write) 또는 트랜잭션 메커니즘(Transactional Mechanism)을 사용하여 기록해야 한다. 이러한 소프트웨어 조치는 쓰기 증폭(Write Amplification)을 감소시키고 예상하지 못한 중단의 영향을 제한하여 SSD에 적용된 기계적·전기적 보호를 보완한다.

저장장치 용량(Storage Capacity)은 명목상 데이터셋 크기만을 기준으로 결정하지 않고 운용 여유(Operational Reserve)를 포함해야 한다. 저장장치의 사용량이 최대 용량에 가까워지면 성능이 저하되고 로깅이나 애플리케이션 서비스에 장애가 발생할 수 있다. 센서 기록 시스템은 보존 정책(Retention Policy), 자동 데이터 전송 또는 오래된 데이터셋 삭제를 통해 일정한 여유 공간을 유지해야 한다. 용량 계획에는 기록 속도, 임무 지속시간, 데이터 업로드 가능 시점, 유지보수 주기 및 통신 장애 동안 보존해야 하는 데이터 양을 포함해야 한다.

SMART 및 NVMe 상태 정보(Health Information)를 로봇 진단 시스템과 통합하면 실제 고장이 발생하기 전에 저장장치의 열화를 감지할 수 있다. 유용한 매개변수에는 온도, 사용 수명 비율(Percentage Used), 예비 용량(Available Spare), 미디어 오류(Media Error), 비정상 종료 횟수(Unsafe Shutdown Count), 누적 동작시간(Power-on Hours), 기록 데이터 단위(Data Units Written), 중요 경고(Critical Warning) 등이 있다. 이러한 정보를 ROS 2 진단 또는 플릿 텔레메트리(Fleet Telemetry)로 모니터링하면 임무 중단이나 데이터 손실이 발생하기 전에 열화된 SSD를 교체할 수 있다.

진동 검증(Vibration Qualification)은 가능하면 실제 로봇의 운용 환경을 반영해야 한다. 실험실에서는 정의된 정현파 진동(Sinusoidal Vibration), 랜덤 진동(Random Vibration), 기계적 충격(Mechanical Shock) 프로파일을 적용할 수 있지만 현장 측정은 바퀴, 서스펜션, 모터, 노면, 매니퓰레이터 및 구조 공진에서 발생하는 실제 가진에 대한 중요한 정보를 제공한다. 엣지 PC 근처에 가속도계(Accelerometer)를 장착하여 실제 진동 스펙트럼(Vibration Spectrum)을 측정하면 보다 대표적인 검증 조건을 설정할 수 있다.

검증은 컴퓨터 전원이 꺼진 상태에서만 수행하지 말고 SSD가 실제로 동작하는 동안 수행해야 한다. 지속적인 쓰기와 읽기, 센서 로깅, PCIe 트래픽 및 열 부하를 진동과 충격 시험 중에도 유지해야 한다. 엔지니어는 파일시스템 오류, NVMe 리셋, PCIe 링크 이벤트, 처리량 변화, 온도 및 애플리케이션 수준의 데이터 손실을 모니터링해야 한다. 이러한 복합 시험(Combined Test)을 통해 독립적인 기계 시험이나 저장장치 벤치마크만으로는 발견하기 어려운 상호작용을 확인할 수 있다.

정비성(Serviceability) 역시 고정 강도(Retention Strength)와 균형을 이루어야 한다. SSD를 컴퓨터 내부에 영구적으로 접착하면 진동에는 강할 수 있지만 현장에서 교체하기 어려워질 수 있다. 양산 설계에서는 규정된 체결부품(Fastener), 토크 사양(Torque Specification), 열 패드, 고정 브래킷(Retention Bracket), 검증 절차를 사용하여 제어된 교체가 가능하도록 해야 한다. 명확한 정비 지침(Service Instruction)을 제공하면 제조 단계에서 확보한 내진동 성능이 유지보수 이후에도 유지되도록 할 수 있다.

강건한 내진동 SSD 아키텍처(Robust Vibration-resistant SSD Architecture)는 적절한 저장 기술, 기계적 고정, 진동 절연, 열 관리, 안정적인 전원, 제어된 종료, 내구성 계획(Endurance Planning), 상태 모니터링 및 실제 환경을 반영한 검증을 통합해야 한다. 목표는 단순히 높은 충격 사양을 가진 SSD를 선정하는 것이 아니라 로봇이 운용 환경에서 지속적으로 연산하고 데이터를 기록하며 이동하는 동안 전체 저장 경로(Storage Path)가 안정적인 신뢰성을 유지하도록 하는 것이다.

로봇 엣지 컴퓨팅(Robotics Edge Computing)에 적합한 저장장치 설계는 로봇의 전체 수명주기 동안 안정적인 PCIe 또는 SATA 연결, 지속적인 쓰기 성능(Sustained Write Performance), 충분한 내구성, 열적 여유(Thermal Margin), 데이터 무결성(Data Integrity)을 유지해야 한다. 기계적 장착과 소프트웨어 관리 역시 이 아키텍처의 중요한 구성요소이다. 이러한 요소들을 통합적으로 설계하면 SSD는 ROS 2 소프트웨어, 지도, AI 모델, 진단 데이터, 센서 데이터셋 및 장시간 피지컬 AI(Physical AI) 운용을 안정적으로 지원하는 신뢰성 높은 기반이 된다.
