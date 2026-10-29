| [KR 한국어](./docs/locales/ko.md) | [US English](./README.md) | [JP 日本語](./docs/locales/ja.md) | [CN 简体中文](./docs/locales/zh-CN.md) | [ES Español](./docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./docs/locales/fr.md) | [DE Deutsch](./docs/locales/de.md) | [RU Русский](./docs/locales/ru.md) | [SA العربية](./docs/locales/ar.md) | [IN हिन्दी](./docs/locales/hi.md) |

---

# Julian Vance (j-vance)

> Senior Systems & Audio DSP Engineer  
> Based in Berlin, Germany · Deterministic real-time architectures, low-latency signal processing kernels, and embedded systems engineering.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 Engineering Overview

I design, measure, and optimize high-throughput, low-latency digital signal processing and systems software. My engineering focus centers on deterministic execution environments where memory allocations on critical audio threads are strictly prohibited, thread synchronization is lock-free, and jitter is eliminated through mechanical sympathy with modern hardware.

- 🎛️ **Primary Domain**: Real-time physical modeling synthesis, analog filter emulations, and SIMD-vectorized DSP pipelines.
- ⚙️ **Hardware Engineering**: Bare-metal embedded audio on STM32H7 (ARM Cortex-M7) and Raspberry Pi RP2040 microcontrollers.
- 📐 **Core Disciplines**: Concurrency without mutexes, cache-line-aware data structures, memory-safe systems programming, and high-assurance verification.
- ☕ **Off-Screen Pursuits**: Restoring 1970s discrete analog preamps, calibrating open-reel tape transport mechanisms, and studying analog filter topologies.

---

## 🏛️ Core Engineering Principles

- **Deterministic Execution**: Zero dynamic memory allocations and strictly bounded execution cycles in real-time hot paths.
- **Lock-Free Concurrency**: Utilizing Single-Producer Single-Consumer (SPSC) ring buffers, sequentially consistent atomics, and explicit memory fences rather than blocking primitives.
- **Hardware Sympathy & Vectorization**: Hand-tuned SIMD intrinsics (AVX2, AVX-512, ARM NEON) structured around contiguous cache lines to maximize memory bandwidth and instruction throughput.
- **Defensive & High-Assurance Design**: Systematic compile-time assertion coverage, runtime sanitization (`ASan`, `UBSan`, `TSan`), and zero-undefined-behavior policies.
- **Minimal Dependencies & Clean Code**: Readable, standards-compliant C++20 and Rust codebases designed for longevity, clarity, and reproducible builds.

---

## 🛠️ Technical Stack & Domain Matrix

### Core Systems & Processing
| Domain | Primary Tools & Languages | Focus Areas & Methodologies |
| :--- | :--- | :--- |
| **Real-Time Systems** | C++20/23, Rust, C99 | Lock-free atomics, zero-allocation hot paths, cache-line alignment |
| **DSP & Vectorization** | AVX2 / AVX-512, ARM NEON, FFTW3 | Biquad cascades, Wave Digital Filters (WDF), polyphase oversampling |
| **Audio Plugin Frameworks** | JUCE 7/8, CLAP, VST3, WebAudio | Custom UI rendering, parameter interpolation smoothing, polyphonic modulation |
| **Embedded & Hardware** | STM32 (ARM Cortex-M7), RP2040, KiCAD | I2S/TDM bus interfacing, Cirrus Logic DAC control, PCB layout design |
| **Analysis & Modeling** | Python, NumPy, SciPy, MATLAB | Frequency response modeling, impulse response analysis, SNR sweeps |
| **Build & Toolchains** | CMake, Ninja, Cargo, LLVM/Clang | Strict sanitizers (`ASan`, `UBSan`), deterministic cross-compilation |

---

## 🚀 Key Open-Source Projects

### 1. `resonant-core` (C++20 / SIMD / CLAP)
A modular, header-only audio DSP library targeting deterministic real-time processing.
- Implements 4x/8x polyphase oversampling filters and non-linear analog ladder filter topologies.
- Native AVX2 and ARM NEON intrinsics with zero memory allocations inside processing blocks.
- Benchmark: 0.18 microseconds per 64-sample block on AMD Zen 4 architecture.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
A continuous-time emulation of magnetic tape saturation and capstan mechanical flutter.
- Physical modeling of hysteretic tape core magnetization using Runge-Kutta 4th-order ODE solvers.
- Cross-compiled to WebAssembly for zero-install, in-browser acoustic research demos.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
Bare-metal synthesizer firmware for custom hardware with full MIDI Polyphonic Expression (MPE) support.
- Dual-core utilization: Core 0 dedicated to USB/DIN-MIDI parsing, Core 1 running a 16-voice subtractive engine at 48kHz.
- Direct DMA feeding to stereo 24-bit I2S DAC without RTOS overhead.

### 4. `ascii-spectrogram` (C99 / Terminal)
A high-performance terminal CLI tool rendering real-time 60 FPS audio waterfalls in ANSI truecolor.
- Lock-free ring buffer directly tapping into ALSA / PulseAudio / PipeWire / CoreAudio streams.
- Optimized windowing functions (Hann, Blackman-Harris) computed entirely via SIMD instructions.

---

## 📊 Current Engineering Benchmarks

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

## 🤝 Collaboration & Contact

I am open to discussions regarding digital signal processing, embedded firmware architecture, low-latency operating systems, and audio hardware prototyping.

- 💬 **Topics I Enjoy**: Lock-free concurrent data structures, discrete transistor modeling, acoustics, analog circuit restorations.
- 📬 **Reach Out**:
  - Email: `julian.vance.audio [at] proton.me`
  - Matrix: `@jvance:matrix.org`
  - GitHub Discussions: Feel free to start a thread on any of my repositories.

---

<sub>Dedicated to deterministic code, clean mathematics, and pure acoustics.</sub>
