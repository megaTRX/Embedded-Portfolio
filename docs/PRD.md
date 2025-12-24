1. 핵심 기술 스택 (기술 역량 증명용)
Language: C (90% 이상), C++ (필요 시 일부 모듈)

Hardware: STM32 (산업계 표준) 또는 ESP32 (Wi-Fi/BT 필요 시)

OS: FreeRTOS (멀티태스킹 및 실시간성 보장 역량 증명)

Protocols: CAN Bus (자동차/선박), Modbus RTU/TCP (공장 자동화), UART/SPI/I2C

Tools: STM32CubeIDE, Logic Analyzer (신호 분석 능력), Git

2. 주요 기능 및 구현 포인트
채용 담당자가 중요하게 보는 '임베디드 개발자의 기본기'를 프로젝트의 기능에 녹여냅니다.

멀티태스킹 설계 (FreeRTOS 활용):

센서 데이터 수집 태스크, 통신 처리 태스크, 시스템 상태 모니터링(Watchdog) 태스크를 분리하여 설계.

증명 포인트: 우선순위 스케줄링 및 태스크 간 동기화(Semaphore, Queue) 이해도.

산업용 표준 통신 구현:

CAN Bus: 노드 간 데이터 송수신 및 필터링 설정 (부산의 선박/차량 산업 타겟).

Modbus RTU: 외부 센서나 PLC와 통신하기 위한 프로토콜 스택 구현.

에러 핸들링 및 결함 허용 (Fault Tolerance):

통신 끊김, 센서 오작동 시 복구 로직(Retry mechanism) 및 HardFault 핸들러 커스텀 구현.

증명 포인트: 하드웨어의 불안정한 환경을 이해하고 대비하는 능력.

저전력 모드 최적화:

시스템 유휴 상태 시 Sleep Mode 진입 및 인터럽트 웨이크업 구현.

3. "테스트 우선" 개발 프로세스 (차별화 포인트)
임베디드 개발에서 가장 중요한 것은 신뢰성입니다. 사용자의 요청대로 테스트를 먼저 고려한 개발 방식을 적용합니다.

Unit Testing: Ceedling이나 Unity 프레임워크를 사용하여 로직별 단위 테스트 코드를 먼저 작성하세요.

Hardware-in-the-Loop (HIL) Test: 실제 센서가 없더라도 신호 발생기로 가상 데이터를 입력하여 시스템이 정상 작동하는지 검증하는 시나리오를 문서화하세요.