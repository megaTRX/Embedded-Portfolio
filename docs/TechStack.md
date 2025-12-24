# 기술 스택 (Tech Stack)

## 📋 개요

이 문서는 임베디드 포트폴리오 프로젝트에서 사용되는 모든 기술 스택을 상세히 설명합니다.

---

## 💻 프로그래밍 언어

### C (Primary - 90%)
- **버전**: C99/C11
- **사용 이유**: 
  - 임베디드 시스템의 사실상 표준 언어
  - 하드웨어 직접 제어 가능
  - 메모리 효율성 및 성능 최적화
  - 산업계에서 가장 널리 사용됨
- **주요 사용처**:
  - 디바이스 드라이버
  - 실시간 태스크 구현
  - 통신 프로토콜 스택
  - 인터럽트 핸들러

### C++ (Secondary - 10%)
- **버전**: C++11/C++14
- **사용 이유**:
  - 객체 지향 설계가 필요한 모듈
  - 코드 재사용성 향상
  - 타입 안정성
- **주요 사용처**:
  - 센서 추상화 레이어
  - 상태 머신 구현
  - 데이터 구조 관리

---

## 🔧 하드웨어 플랫폼

### STM32 (Primary)
- **모델**: STM32F4xx 시리즈 권장
  - STM32F407VG (168MHz, 1MB Flash, 192KB RAM)
  - STM32F429ZI (180MHz, 2MB Flash, 256KB RAM)
- **선택 이유**:
  - 산업계 표준 MCU
  - 풍부한 주변장치 (CAN, UART, SPI, I2C, ADC, DAC)
  - 강력한 개발 도구 지원
  - 대규모 커뮤니티 및 레퍼런스
- **개발 보드**:
  - STM32 Nucleo-F429ZI
  - STM32F4 Discovery
  - 커스텀 PCB (선택사항)

### ESP32 (Alternative)
- **모델**: ESP32-WROOM-32
- **선택 이유**:
  - Wi-Fi/Bluetooth 내장
  - 저렴한 가격
  - Arduino 호환성
- **사용 시나리오**:
  - 무선 통신이 필요한 경우
  - IoT 기능 확장 시
  - 빠른 프로토타이핑

---

## 🖥️ 실시간 운영체제 (RTOS)

### FreeRTOS
- **버전**: FreeRTOS 10.x 이상
- **라이선스**: MIT License
- **주요 기능**:
  - ✅ 선점형 멀티태스킹
  - ✅ 우선순위 기반 스케줄링
  - ✅ Semaphore, Mutex, Queue
  - ✅ 소프트웨어 타이머
  - ✅ 이벤트 그룹
- **선택 이유**:
  - 업계 표준 RTOS
  - 작은 메모리 풋프린트 (4-9KB)
  - 풍부한 문서 및 예제
  - 상용 제품에 널리 사용됨
- **설정**:
  - Heap: Heap_4 (메모리 단편화 방지)
  - Tick Rate: 1000Hz (1ms)
  - Max Priorities: 5-7

---

## 📡 통신 프로토콜

### 1. CAN Bus
- **표준**: CAN 2.0A/2.0B
- **Baud Rate**: 500 kbps (권장)
- **하드웨어**:
  - CAN 컨트롤러: STM32 내장 bxCAN
  - CAN 트랜시버: MCP2551, TJA1050
- **라이브러리**: 
  - STM32 HAL CAN Driver
  - 커스텀 CAN 프로토콜 스택
- **적용 분야**:
  - 자동차 ECU 통신
  - 선박 제어 시스템
  - 산업용 네트워크

### 2. Modbus RTU
- **표준**: Modbus RTU (Serial)
- **인터페이스**: RS-485
- **Baud Rate**: 9600, 19200, 115200 bps
- **하드웨어**:
  - UART: STM32 내장 USART
  - RS-485 트랜시버: MAX485, SN75176
- **구현**:
  - 커스텀 Modbus 스택
  - CRC-16 체크섬
  - 마스터/슬레이브 모드
- **적용 분야**:
  - PLC 통신
  - 센서/액추에이터 제어
  - 공장 자동화

### 3. Modbus TCP (선택사항)
- **표준**: Modbus TCP/IP
- **포트**: 502
- **TCP/IP 스택**: lwIP (Lightweight IP)
- **적용 분야**:
  - 이더넷 기반 제어 시스템
  - SCADA 시스템 연동

### 4. UART/SPI/I2C
- **UART**: 
  - 디버그 로그 출력
  - GPS, Bluetooth 모듈 통신
- **SPI**:
  - 고속 센서 통신
  - SD 카드 인터페이스
  - 디스플레이 제어
- **I2C**:
  - 센서 통신 (온도, 압력, 가속도계)
  - EEPROM 접근
  - RTC (Real-Time Clock)

### 5. Wi-Fi/Bluetooth (ESP32)
- **Wi-Fi**: 802.11 b/g/n
- **Bluetooth**: BLE 4.2, Classic Bluetooth
- **프로토콜**:
  - MQTT (IoT 통신)
  - HTTP/HTTPS (웹 서버)
  - WebSocket (실시간 데이터)

---

## 🛠️ 개발 도구

### IDE (통합 개발 환경)
- **STM32CubeIDE**
  - 버전: 1.13.x 이상
  - 기반: Eclipse
  - 주요 기능:
    - 코드 편집 및 디버깅
    - STM32CubeMX 통합
    - GDB 디버거
    - 성능 분석 도구

### 코드 생성 도구
- **STM32CubeMX**
  - 핀 설정 및 클록 구성
  - 주변장치 초기화 코드 생성
  - FreeRTOS 설정

### 컴파일러
- **ARM GCC**
  - 버전: arm-none-eabi-gcc 10.x 이상
  - 최적화 레벨: -O2 (릴리스), -Og (디버그)

### 디버거
- **ST-Link V2/V3**
  - SWD (Serial Wire Debug) 인터페이스
  - 실시간 디버깅
  - 플래시 프로그래밍

### 신호 분석 도구
- **Logic Analyzer**
  - Saleae Logic 8
  - 또는 저가형 USB Logic Analyzer
  - 프로토콜 디코딩 (UART, SPI, I2C, CAN)
- **Oscilloscope**
  - 아날로그 신호 분석
  - 타이밍 검증

---

## 🧪 테스트 프레임워크

### Unit Testing
- **Unity Test Framework**
  - C 언어용 경량 테스트 프레임워크
  - 임베디드 시스템에 최적화
  - GitHub: ThrowTheSwitch/Unity

### Test Runner
- **Ceedling**
  - Unity 기반 빌드 자동화
  - Mock 생성 (CMock)
  - 코드 커버리지 (gcov)

### 통합 테스트
- **HIL (Hardware-in-the-Loop)**
  - 신호 발생기를 통한 가상 입력
  - 실제 하드웨어 환경 시뮬레이션
- **SIL (Software-in-the-Loop)**
  - PC 환경에서 소프트웨어 테스트
  - QEMU ARM 에뮬레이터 (선택사항)

---

## 📊 빌드 및 자동화

### 빌드 시스템
- **Make**
  - Makefile 기반 빌드
  - 크로스 컴파일 설정
- **CMake** (선택사항)
  - 크로스 플랫폼 빌드
  - 테스트 통합

### 버전 관리
- **Git**
  - GitHub / GitLab
  - Branching Strategy: Git Flow
  - Commit Convention: Conventional Commits

### CI/CD
- **GitHub Actions**
  - 자동 빌드
  - 단위 테스트 실행
  - 코드 품질 검사
- **Jenkins** (선택사항)
  - 자체 호스팅 CI/CD

---

## 📚 라이브러리 및 미들웨어

### STM32 HAL (Hardware Abstraction Layer)
- STM32 Cube HAL 드라이버
- 주변장치 추상화
- 이식성 향상

### lwIP (Lightweight IP)
- TCP/IP 스택
- Modbus TCP 구현에 사용
- 메모리 효율적

### FatFs
- FAT 파일 시스템
- SD 카드 데이터 로깅
- 설정 파일 관리

### TensorFlow Lite Micro (선택사항)
- 엣지 AI/ML
- 센서 데이터 분석
- 예측 유지보수

---

## 🔐 보안 (선택사항)

### 암호화 라이브러리
- **mbedTLS**
  - TLS/SSL 구현
  - AES, RSA 암호화
  - 인증서 관리

### Secure Boot
- STM32 보안 기능 활용
- 펌웨어 서명 검증
- 읽기 보호 (RDP)

---

## 📝 문서화 도구

### 코드 문서화
- **Doxygen**
  - API 문서 자동 생성
  - HTML/PDF 출력
  - 그래프 생성 (Graphviz)

### 다이어그램
- **PlantUML**
  - UML 다이어그램
  - 시퀀스 다이어그램
  - 클래스 다이어그램
- **Draw.io**
  - 시스템 아키텍처
  - 블록 다이어그램
  - 회로도

### 마크다운
- **Markdown**
  - README, 기술 문서
  - GitHub 호환
- **Marp** (선택사항)
  - 마크다운 기반 프레젠테이션

---

## 🔍 코드 품질 도구

### 정적 분석
- **Cppcheck**
  - C/C++ 정적 분석
  - 버그 및 취약점 탐지
- **Clang-Tidy**
  - 코드 스타일 검사
  - 모던 C++ 권장사항

### 코드 포맷팅
- **clang-format**
  - 일관된 코드 스타일
  - .clang-format 설정 파일

### 코드 커버리지
- **gcov / lcov**
  - 테스트 커버리지 측정
  - HTML 리포트 생성

---

## 🌐 IoT 및 클라우드 (선택사항)

### MQTT
- **Mosquitto**
  - MQTT 브로커
  - Pub/Sub 메시징
- **Paho MQTT**
  - MQTT 클라이언트 라이브러리

### 클라우드 플랫폼
- **AWS IoT Core**
  - 디바이스 관리
  - 데이터 수집 및 분석
- **Azure IoT Hub**
  - 엔터프라이즈급 IoT 솔루션
- **ThingSpeak**
  - 간단한 데이터 시각화

---

## 📦 패키지 관리

### 의존성 관리
- **Git Submodules**
  - 외부 라이브러리 관리
  - FreeRTOS, Unity 등
- **PlatformIO** (ESP32)
  - 라이브러리 관리
  - 멀티 플랫폼 지원

---

## 🎯 기술 스택 선택 기준

### 산업 표준 준수
- ✅ 자동차, 선박, 공장 자동화 산업에서 널리 사용
- ✅ 장기적인 지원 및 안정성

### 학습 및 커리어 가치
- ✅ 취업 시장에서 요구되는 기술
- ✅ 실무 프로젝트에 바로 적용 가능

### 포트폴리오 차별화
- ✅ 테스트 우선 개발 (Unit Testing, HIL)
- ✅ 신뢰성 및 안정성 중심 설계
- ✅ 산업용 프로토콜 구현 경험

### 확장성
- ✅ IoT, AI/ML 등 최신 기술 통합 가능
- ✅ 다양한 산업 분야 적용 가능

---

## 📊 기술 스택 매트릭스

| 카테고리 | 기술 | 필수/선택 | 난이도 | 산업 관련성 |
|---------|------|----------|--------|------------|
| 언어 | C | 필수 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 언어 | C++ | 선택 | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| MCU | STM32 | 필수 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| MCU | ESP32 | 선택 | ⭐⭐ | ⭐⭐⭐ |
| RTOS | FreeRTOS | 필수 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 통신 | CAN Bus | 필수 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 통신 | Modbus RTU | 필수 | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 통신 | Modbus TCP | 선택 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| 테스트 | Unity | 필수 | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| 테스트 | HIL | 권장 | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| 보안 | mbedTLS | 선택 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ |
| IoT | MQTT | 선택 | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| AI | TF Lite Micro | 선택 | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |

---

## 🚀 학습 경로

### 초급 (1-2주)
1. C 언어 기초 복습
2. STM32 개발 환경 설정
3. GPIO, UART 기본 예제
4. Git 기본 사용법

### 중급 (3-4주)
1. FreeRTOS 기초 (태스크, 큐, 세마포어)
2. UART, SPI, I2C 통신
3. 인터럽트 및 타이머
4. Unity 테스트 프레임워크

### 고급 (5-8주)
1. CAN Bus 프로토콜 구현
2. Modbus RTU 스택 개발
3. 에러 핸들링 및 결함 허용
4. 저전력 모드 최적화
5. HIL 테스트 환경 구축

### 전문가 (9주 이상)
1. Modbus TCP 및 lwIP
2. 보안 기능 (암호화, Secure Boot)
3. IoT 클라우드 연동
4. 엣지 AI/ML 통합

---

## 📖 참고 자료

### 공식 문서
- [STM32 Documentation](https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html)
- [FreeRTOS Documentation](https://www.freertos.org/Documentation/RTOS_book.html)
- [Modbus Specification](https://modbus.org/specs.php)
- [CAN Bus Specification](https://www.can-cia.org/)

### 온라인 강의
- Udemy: "Mastering RTOS: Hands on FreeRTOS"
- Coursera: "Introduction to Embedded Systems"
- YouTube: STM32 튜토리얼 채널

### 서적
- "The Definitive Guide to ARM Cortex-M3 and Cortex-M4"
- "Mastering the FreeRTOS Real Time Kernel"
- "Embedded C Coding Standard"

### 커뮤니티
- STM32 Community Forum
- FreeRTOS Forum
- Stack Overflow (embedded tag)
- Reddit: r/embedded

---

## 🔄 버전 관리

| 버전 | 날짜 | 변경 내용 |
|------|------|----------|
| 1.0 | 2024-12-24 | 초기 버전 작성 |

---

## 📞 문의

기술 스택 관련 질문이나 제안사항이 있으시면 GitHub Issues를 통해 문의해주세요.
