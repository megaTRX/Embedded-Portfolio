# Embedded Portfolio - 산업용 실시간 제어 시스템

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Language: C](https://img.shields.io/badge/Language-C-blue.svg)](https://en.wikipedia.org/wiki/C_(programming_language))
[![RTOS: FreeRTOS](https://img.shields.io/badge/RTOS-FreeRTOS-green.svg)](https://www.freertos.org/)
[![MCU: STM32](https://img.shields.io/badge/MCU-STM32-red.svg)](https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html)

> 임베디드 개발자의 핵심 역량을 증명하는 산업용 실시간 제어 시스템 포트폴리오 프로젝트

## 🎯 프레젝트 프레젠테이션

### 📊 온라인 프레젠테이션 보기
👉 **[프레젠테이션 바로가기](https://megatrx.github.io/Embedded-Portfolio/)**

프로젝트의 전체 내용을 웹 프레젠테이션으로 확인하실 수 있습니다.

---

## 📋 프로젝트 개요

이 프로젝트는 **산업 현장에서 실제로 요구되는 임베디드 개발 역량**을 종합적으로 보여주는 포트폴리오입니다. 단순한 데모가 아닌, 자동차, 선박, 공장 자동화 등 실제 산업 분야에서 사용 가능한 수준의 시스템을 구현합니다.

### 🎯 프로젝트 목표

- ✅ **실시간 멀티태스킹 시스템** 설계 및 구현 (FreeRTOS)
- ✅ **산업용 통신 프로토콜** 구현 (CAN Bus, Modbus RTU/TCP)
- ✅ **안정성 및 신뢰성** 확보 (에러 핸들링, 결함 허용)
- ✅ **저전력 최적화** 구현
- ✅ **테스트 우선 개발** 방법론 적용 (Unit Testing, HIL Testing)

### 🏭 타겟 산업

- 🚢 **선박/해양 산업** - CAN Bus 기반 제어 시스템
- 🚗 **자동차 산업** - ECU 통신 및 센서 데이터 처리
- 🏭 **공장 자동화** - Modbus 기반 PLC 통신

---

## 🛠️ 핵심 기술 스택

### 프로그래밍 언어
- **C** (90% 이상) - 임베디드 시스템의 표준 언어
- **C++** (10%) - 객체 지향 모듈 구현

### 하드웨어 플랫폼
- **STM32F4xx** (Primary) - 산업계 표준 MCU
  - STM32F407VG (168MHz, 1MB Flash, 192KB RAM)
  - STM32F429ZI (180MHz, 2MB Flash, 256KB RAM)
- **ESP32** (Alternative) - Wi-Fi/Bluetooth 통신용

### 실시간 운영체제
- **FreeRTOS 10.x** - 멀티태스킹 및 실시간성 보장
  - 선점형 스케줄링
  - 우선순위 기반 태스크 관리
  - Semaphore, Mutex, Queue

### 통신 프로토콜
- **CAN Bus** (CAN 2.0A/2.0B) - 자동차/선박 산업 표준
- **Modbus RTU** - 공장 자동화 표준 (RS-485)
- **Modbus TCP** - 이더넷 기반 제어 시스템
- **UART/SPI/I2C** - 기본 통신 인터페이스

### 개발 도구
- **STM32CubeIDE** - 통합 개발 환경
- **STM32CubeMX** - 하드웨어 설정 도구
- **Logic Analyzer** - 신호 분석 및 디버깅
- **Git** - 버전 관리

### 테스트 프레임워크
- **Unity** - C 언어용 단위 테스트 프레임워크
- **Ceedling** - 테스트 자동화 및 빌드 시스템
- **HIL (Hardware-in-the-Loop)** - 실제 환경 시뮬레이션

> 📚 **상세한 기술 스택 정보**: [TechStack.md](docs/TechStack.md) 참조

---

## 🎯 주요 기능

### 1️⃣ FreeRTOS 기반 멀티태스킹 설계

```c
// 태스크 구조
┌─────────────────────────────────────┐
│      FreeRTOS Scheduler             │
├───────────┬───────────┬─────────────┤
│  Sensor   │   Comm    │  Monitor    │
│  Task     │   Task    │  Task       │
│  (High)   │  (Medium) │  (Low)      │
└───────────┴───────────┴─────────────┘
```

**구현 내용**:
- 📊 센서 데이터 수집 태스크 (주기: 100ms)
- 📡 통신 처리 태스크 (CAN/Modbus)
- 🔍 시스템 모니터링 태스크 (Watchdog)
- 🔄 태스크 간 동기화 (Semaphore, Queue, Mutex)

### 2️⃣ CAN Bus 통신 구현

**기능**:
- CAN 2.0A/2.0B 표준 준수
- 500 kbps 통신 속도
- ID 기반 필터링 설정
- 에러 감지 및 복구 (Bus-off recovery)

**적용 분야**:
- 자동차 ECU 간 통신
- 선박 제어 시스템
- 산업용 네트워크

### 3️⃣ Modbus RTU/TCP 프로토콜 스택

**구현 펑션 코드**:
- `0x03`: Read Holding Registers
- `0x04`: Read Input Registers
- `0x06`: Write Single Register
- `0x10`: Write Multiple Registers

**특징**:
- 커스텀 Modbus 스택 개발
- CRC-16 체크섬 검증
- 마스터/슬레이브 모드 지원
- RS-485 인터페이스

### 4️⃣ 에러 핸들링 및 결함 허용

**복구 메커니즘**:
- ✅ 통신 끊김 시 Retry 로직 (지수 백오프)
- ✅ 센서 오작동 감지 및 Fallback
- ✅ HardFault 핸들러 커스텀 구현
- ✅ Watchdog 타이머 (IWDG, WWDG)

### 5️⃣ 저전력 모드 최적화

**전력 관리**:
- 시스템 유휴 상태 감지
- Sleep Mode 자동 진입
- 인터럽트 기반 웨이크업
- 주변장치 선택적 활성화

**효과**:
- 🔋 배터리 수명 30% 이상 연장
- 🌡️ 발열 감소
- ⚡ 에너지 효율성 향상

---

## 🧪 테스트 우선 개발 프로세스

### 차별화 포인트

> 임베디드 개발에서 가장 중요한 것은 **신뢰성**입니다.  
> 이 프로젝트는 테스트를 먼저 고려한 개발 방식을 적용합니다.

### Unit Testing

**프레임워크**: Unity + Ceedling

**방법론**:
1. 테스트 코드 우선 작성 (TDD)
2. 각 모듈의 독립적 검증
3. 코드 커버리지 80% 이상 목표
4. CI/CD 파이프라인 통합

### Hardware-in-the-Loop (HIL) Testing

**테스트 환경**:
- 신호 발생기를 통한 가상 센서 데이터 입력
- 실제 하드웨어 환경 시뮬레이션
- 엣지 케이스 및 오류 상황 테스트

**문서화**:
- 테스트 시나리오 상세 기록
- 검증 결과 데이터 수집
- 재현 가능한 테스트 환경 구축

---

## 📊 프로젝트 성과 지표

| 항목 | 목표 | 설명 |
|------|------|------|
| ⏱️ 태스크 응답 시간 | < 10ms | 실시간성 보장 |
| 📡 통신 성공률 | > 99.9% | 안정적인 통신 |
| 🔋 전력 소비 감소 | > 30% | 저전력 최적화 |
| 🧪 코드 커버리지 | > 80% | 테스트 품질 |
| 🔧 MTBF | > 1000시간 | 평균 고장 간격 |

---

## 📁 프로젝트 구조

```
Embedded-Portfolio/
├── docs/                      # 📚 문서
│   ├── README.md             # 프로젝트 개요
│   ├── PRD.md                # 제품 요구사항 정의
│   ├── TechStack.md          # 기술 스택 상세
│   ├── task.md               # 작업 목록 (151개 태스크)
│   ├── tool.md               # 도구 및 키트 가이드
│   ├── presentation.md       # 프로젝트 프레젠테이션
│   └── presentation.pptx.md  # Marp 슬라이드
├── src/                       # 💻 소스 코드
│   ├── main.c                # 메인 애플리케이션
│   ├── tasks/                # FreeRTOS 태스크
│   ├── drivers/              # 하드웨어 드라이버
│   ├── protocols/            # 통신 프로토콜
│   └── utils/                # 유틸리티 함수
├── inc/                       # 📄 헤더 파일
├── test/                      # 🧪 테스트 코드
│   ├── unit/                 # 단위 테스트
│   └── integration/          # 통합 테스트
├── hardware/                  # 🔌 하드웨어 문서
│   ├── schematics/           # 회로도
│   └── datasheets/           # 데이터시트
├── .github/                   # ⚙️ GitHub 설정
│   └── workflows/            # CI/CD 파이프라인
├── Makefile                   # 🔨 빌드 스크립트
└── README.md                  # 프로젝트 루트 README
```

---

## 🚀 시작하기

### 필수 요구사항

#### 하드웨어
- STM32 개발 보드 (F4xx 시리즈 권장)
- ST-Link V2/V3 디버거
- CAN 트랜시버 (MCP2551 또는 TJA1050)
- RS-485 트랜시버 (MAX485 또는 SN75176)
- Logic Analyzer (선택사항)

#### 소프트웨어
- STM32CubeIDE 1.13.x 이상
- Git
- ARM GCC Toolchain (STM32CubeIDE에 포함)
- Unity Test Framework
- Make

### 설치 및 빌드

```bash
# 1. 저장소 클론
git clone https://github.com/megaTRX/Embedded-Portfolio.git
cd Embedded-Portfolio

# 2. 서브모듈 초기화 (FreeRTOS, Unity 등)
git submodule update --init --recursive

# 3. 빌드
make all

# 4. 플래시 프로그래밍
make flash

# 5. 테스트 실행
make test
```

### STM32CubeIDE에서 열기

1. STM32CubeIDE 실행
2. `File` → `Open Projects from File System`
3. 프로젝트 디렉토리 선택
4. `Finish` 클릭
5. `Project` → `Build Project`

---

## 📖 문서

### 핵심 문서
- 📄 **[PRD.md](docs/PRD.md)** - 제품 요구사항 정의서
- 🛠️ **[TechStack.md](docs/TechStack.md)** - 기술 스택 상세 문서
- 🔧 **[tool.md](docs/tool.md)** - 도구 및 키트 가이드
- ✅ **[task.md](docs/task.md)** - 구현 작업 목록 (10 Phases, 151 Tasks)
- 📊 **[presentation.md](docs/presentation.md)** - 프로젝트 프레젠테이션
- 🎨 **[presentation.pptx.md](docs/presentation.pptx.md)** - Marp 슬라이드

### API 문서
- Doxygen으로 생성된 API 문서 (빌드 후 `docs/api` 폴더)

### 테스트 문서
- 테스트 계획서
- 테스트 케이스
- HIL 테스트 시나리오

---

## 🎓 학습 경로

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

## 🔄 개발 프로세스

### Agile & Test-Driven Development

```
요구사항 분석 → 테스트 작성 → 코드 구현 → 테스트 실행
     ↑                                            ↓
     └──────────── 리팩토링 ← 문서화 ← 통과? ──────┘
```

### Git Workflow

- **main** - 안정 버전
- **develop** - 개발 브랜치
- **feature/** - 기능 개발
- **bugfix/** - 버그 수정
- **release/** - 릴리스 준비

### Commit Convention

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

---

## 🚀 향후 확장 계획

### Phase 10: 확장 기능 (선택사항)

- 📱 **무선 통신**: Wi-Fi/Bluetooth를 통한 원격 모니터링
- 🔐 **보안**: 통신 암호화 (mbedTLS) 및 Secure Boot
- 📈 **데이터 로깅**: SD 카드 또는 Flash 메모리 활용
- 🌐 **IoT 연동**: MQTT, AWS IoT Core, Azure IoT Hub
- 🤖 **AI/ML**: TensorFlow Lite Micro를 통한 엣지 AI

---

## 💡 프로젝트의 핵심 가치

### 임베디드 개발자의 기본기 증명

| 역량 | 구현 내용 | 증명 포인트 |
|------|----------|------------|
| ⚙️ **실시간 시스템** | FreeRTOS 멀티태스킹 | 우선순위 스케줄링, 동기화 |
| 📡 **산업 표준** | CAN Bus, Modbus | 프로토콜 스택 직접 구현 |
| 🛡️ **안정성** | 에러 핸들링 & 결함 허용 | 불안정한 환경 대비 능력 |
| ⚡ **최적화** | 저전력 모드 | 전력 소비 30% 감소 |
| 🧪 **품질** | Unit Testing & HIL | 테스트 우선 개발 방법론 |

---

## 📊 프로젝트 타임라인

| Phase | 기간 | 주요 활동 | 상태 |
|-------|------|----------|------|
| 1. 프로젝트 설정 | 1-2일 | 환경 구축, 테스트 프레임워크 | ⏳ |
| 2. FreeRTOS 구현 | 5-7일 | 멀티태스킹, 동기화 | ⏳ |
| 3. CAN Bus | 3-4일 | CAN 드라이버, 프로토콜 | ⏳ |
| 4. Modbus | 3-4일 | Modbus RTU/TCP 스택 | ⏳ |
| 5. 에러 핸들링 | 2-3일 | Fault Tolerance | ⏳ |
| 6. 저전력 최적화 | 2-3일 | Sleep Mode, 전력 관리 | ⏳ |
| 7. 테스트 | 4-5일 | Unit Test, HIL Test | ⏳ |
| 8. 문서화 | 2-3일 | API 문서, 사용자 가이드 | ✅ |
| 9. 데모 준비 | 1-2일 | 영상, 스크린샷 | ⏳ |
| 10. 확장 기능 | 선택 | IoT, AI/ML, 보안 | ⏳ |

**총 예상 기간**: 약 1개월 (23-33일)

---

## 🤝 기여하기

이 프로젝트는 학습 및 포트폴리오 목적으로 개발되었습니다. 기여를 환영합니다!

### 기여 방법

1. 이 저장소를 Fork 합니다
2. Feature 브랜치를 생성합니다 (`git checkout -b feature/AmazingFeature`)
3. 변경사항을 커밋합니다 (`git commit -m 'feat: Add some AmazingFeature'`)
4. 브랜치에 Push 합니다 (`git push origin feature/AmazingFeature`)
5. Pull Request를 생성합니다

### 코딩 컨벤션

- C99/C11 표준 준수
- 들여쓰기: 4 spaces
- 함수명: `snake_case`
- 매크로: `UPPER_CASE`
- 주석: Doxygen 스타일

---

## 📜 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

## 📞 연락처 및 리소스

### GitHub Repository
🔗 [https://github.com/megaTRX/Embedded-Portfolio](https://github.com/megaTRX/Embedded-Portfolio)

### 프레젠테이션
🎯 [온라인 프레젠테이션 보기](https://megatrx.github.io/Embedded-Portfolio/)

### 문의
- GitHub Issues를 통한 버그 리포트 및 기능 제안
- Pull Request를 통한 코드 기여

### 참고 자료

#### 공식 문서
- [STM32 Documentation](https://www.st.com/en/microcontrollers-microprocessors/stm32-32-bit-arm-cortex-mcus.html)
- [FreeRTOS Documentation](https://www.freertos.org/Documentation/RTOS_book.html)
- [Modbus Specification](https://modbus.org/specs.php)
- [CAN Bus Specification](https://www.can-cia.org/)

#### 온라인 강의
- Udemy: "Mastering RTOS: Hands on FreeRTOS"
- Coursera: "Introduction to Embedded Systems"

#### 커뮤니티
- [STM32 Community Forum](https://community.st.com/)
- [FreeRTOS Forum](https://forums.freertos.org/)
- [Stack Overflow - embedded](https://stackoverflow.com/questions/tagged/embedded)
- [Reddit - r/embedded](https://www.reddit.com/r/embedded/)

---

## 🎯 결론

### 왜 이 프로젝트인가?

> 이 포트폴리오 프로젝트는 단순한 데모가 아닌,  
> **실제 산업 현장에서 요구되는 임베디드 개발 역량**을  
> 종합적으로 보여줍니다.

### 핵심 메시지

**신뢰성 있는 실시간 시스템을 설계하고,**  
**산업 표준을 준수하며,**  
**체계적인 테스트로 검증할 수 있는 개발자**

---

## 📈 프로젝트 진행 상황

![Progress](https://img.shields.io/badge/Progress-Planning-yellow)
![Documentation](https://img.shields.io/badge/Documentation-Complete-green)
![Implementation](https://img.shields.io/badge/Implementation-Pending-orange)

**마지막 업데이트**: 2024-12-24

---

## ⭐ Star History

이 프로젝트가 도움이 되었다면 ⭐️를 눌러주세요!

---

**Made with ❤️ by megaTRX**

**Embedded Systems Portfolio Project**  
**Industrial Real-Time Control System**
