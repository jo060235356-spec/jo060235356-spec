| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# 줄리안 밴스 (Julian Vance / j-vance)

> 시니어 시스템 & 오디오 DSP 엔지니어  
> 독일 베를린 거주 · 결정론적 실시간 아키텍처, 초저지연 DSP 커널, 베어메탈 임베디드 시스템 전문

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 엔지니어링 개요

고처리량·초저지연 디지털 신호 처리와 시스템 소프트웨어를 설계하고 측정하며 최적화합니다. 핵심 오디오 스레드 내에서의 동적 메모리 할당을 전면 배제하고, 뮤텍스 없는 락프리 동기화를 적용하며, 하드웨어 특성을 반영한 캐시 친화적 설계를 통해 지터(Jitter)를 원천 차단하는 결정론적 런타임 구축에 집중하고 있습니다.

- 🎛️ **주요 전문 분야**: 실시간 물리 모델링 음향 합성, 아날로그 필터 회로 시뮬레이션, SIMD 벡터화 DSP 파이프라인.
- ⚙️ **하드웨어 엔지니어링**: STM32H7 (ARM Cortex-M7) 및 Raspberry Pi RP2040 기반 베어메탈 오디오 시스템.
- 📐 **핵심 설계 규율**: 락프리 동시성 제어, 캐시 라인 정렬 자료구조, 고신뢰 메모리 안전성, 엄격한 정적/동적 검증.
- ☕ **화면 밖의 일상**: 1970년대 아날로그 프리앰프 회로 복원, 오픈 릴 테이프 기계 부품 캘리브레이션, 음향 필터 구조 연구.

---

## 🏛️ 핵심 엔지니어링 원칙

- **결정론적 실행 (Deterministic Execution)**: 실시간 핫 패스 내에서 동적 메모리 할당 제로(Zero-Allocation) 및 엄격히 제한된 실행 사이클 보장.
- **락프리 동시성 (Lock-Free Concurrency)**: 블로킹 프리미티브 대신 단일 생산자-단일 소비자(SPSC) 링 버퍼, 순차 일관성 원자 연산, 명시적 메모리 펜스 활용.
- **하드웨어 친화적 벡터화 (Hardware Sympathy & SIMD)**: 캐시 라인 연속성을 고려하여 직접 튜닝된 AVX2, AVX-512, ARM NEON 고속 연산 커널 적용.
- **고신뢰 방어적 설계 (High-Assurance Design)**: 컴파일 타임 단언(Assertions) 전수 적용, 런타임 새니타이저(`ASan`, `UBSan`, `TSan`) 상시 검증, 정의되지 않은 동작(UB) 배제.
- **최소 의존성과 유지보수성**: 불필요한 서드파티 프레임워크를 지양하고, 표준 C++20과 Rust 기반의 간결하고 재현 가능한 코드베이스 유지.

---

## 🛠️ 기술 스택 및 도메인 매트릭스

### 코어 시스템 및 신호 처리
| 도메인 | 핵심 도구 및 프로그래밍 언어 | 중점 영역 및 방법론 |
| :--- | :--- | :--- |
| **실시간 시스템** | C++20/23, Rust, C99 | 락프리 원자적 연산, 제로 할당 핫 패스, CPU 캐시 라인 정렬 |
| **DSP 및 벡터화** | AVX2 / AVX-512, ARM NEON, FFTW3 | 바이쿼드 캐스케이드, 웨이브 디지털 필터(WDF), 폴리페이즈 오버샘플링 |
| **오디오 플러그인** | JUCE 7/8, CLAP, VST3, WebAudio | 커스텀 UI 렌더링, 파라미터 보간 스무딩, 다성부 모듈레이션 구조 |
| **임베디드 및 하드웨어** | STM32 (ARM Cortex-M7), RP2040, KiCAD | I2S/TDM 버스 인터페이스, Cirrus Logic DAC 제어, 회로도 아트워크 설계 |
| **분석 및 모델링** | Python, NumPy, SciPy, MATLAB | 주파수 응답 수치 해석, 임펄스 응답 분석, 왜곡 및 신호 대 잡음비(SNR) 측정 |
| **빌드 및 툴체인** | CMake, Ninja, Cargo, LLVM/Clang | 엄격한 새니타이저(`ASan`, `UBSan`), 결정론적 크로스 컴파일 |

---

## 🚀 주요 오픈소스 프로젝트

### 1. `resonant-core` (C++20 / SIMD / CLAP)
결정론적 실시간 신호 처리를 지향하는 모듈형 헤더 온리 오디오 DSP 라이브러리.
- 4x/8x 폴리페이즈 오버샘플링 필터 및 비선형 아날로그 래더 필터 토폴로지 구현.
- 처리 블록 내부 메모리 할당이 전혀 없는 순수 AVX2 및 ARM NEON 내장 함수 가속.
- 벤치마크: AMD Zen 4 아키텍처 환경에서 64 샘플 블록당 0.18 마이크로초 소요.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
자기 테이프의 자기 포화(Saturation) 현상과 캡스턴 모터의 기계적 플러터(Flutter)를 연속 시간으로 에뮬레이션한 오디오 프로세서.
- 4차 룽게-쿠타(RK4) 미분방정식 솔버 기반 자화 히스테리시스 물리 모델링.
- 별도 설치 없이 브라우저에서 바로 음향 특성을 테스트할 수 있는 WebAssembly 크로스 빌드 지원.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
MPE(MIDI Polyphonic Expression)를 완벽히 지원하는 커스텀 하드웨어용 베어메탈 신디사이저 펌웨어.
- 듀얼 코어 분할 활용: Core 0는 USB/DIN-MIDI 파싱 전담, Core 1은 48kHz 16-보이스 서브트랙티브 엔진 구동.
- RTOS 오버헤드 없이 스테레오 24-bit I2S DAC로 직접 DMA 스트리밍 전송.

### 4. `ascii-spectrogram` (C99 / Terminal)
ANSI 트루컬러를 통해 60 FPS 실시간 오디오 워터폴을 렌더링하는 고성능 터미널 CLI 도구.
- ALSA / PulseAudio / PipeWire / CoreAudio 오디오 스트림에 직접 연결되는 락프리 링 버퍼.
- SIMD 벡터 명령어로 최적화 계산되는 고속 윈도우 함수(Hann, Blackman-Harris).

---

## 📊 현재 엔지니어링 벤치마크

```text
[CURRENT WORKSPACE BENCHMARKS - 64 SAMPLES @ 96 kHz]
+-------------------------+----------------+----------------+------------+
| Module                  | Algorithm      | Hot-Loop Time  | Memory I/O |
+-------------------------+----------------+----------------+------------+
| Tape Hysteresis Sat     | RK4 / Non-lin  |   142 ns / smp |   0 alloc  |
| 4-Pole Moog Ladder WDF  | Trapezoidal    |    88 ns / smp |   0 alloc  |
| Polyphase Resampler 4x  | 64-tap Poly    |    34 ns / smp |   0 alloc  |
| Stereophonic Reverb     | FDN 16-channel |   210 ns / smp |   0 alloc  |
+-------------------------+----------------+----------------+------------+
* Measured using LLVM 18 with -O3 -march=native on Linux 6.8 lowlatency kernel.
```

---

## 🤝 협업 및 문의

디지털 신호 처리, 임베디드 펌웨어 아키텍처, 저지연 운영체제 최적화, 오디오 하드웨어 프로토타이핑에 관한 기술적 논의를 환영합니다.

- 💬 **주요 관심 주제**: 락프리 동시성 자료구조, 아날로그 소자 물리 모델링, 공간 음향학, 빈티지 음향 기기 복원.
- 📬 **연락처**:
  - Email: `julian.vance.audio [at] proton.me`
  - Matrix: `@jvance:matrix.org`
  - GitHub Discussions: 저장소의 토론 탭을 통해 자유롭게 스레드를 개설하실 수 있습니다.

---

<sub>결정론적 코드, 명료한 수학, 순수한 음향학을 지향합니다.</sub>
