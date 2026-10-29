# GitLab Profile Specification: Julian Vance

## 1. Profile Settings (Settings -> Profile)

- **Full Name**: Julian Vance
- **Job Title**: Audio DSP Systems Engineer
- **Bio**: Audio DSP & low-latency systems engineer based in Berlin. Building deterministic real-time audio pipelines, embedded DSP firmware (STM32/RP2040), and physical modeling plugins. Zero allocations in the audio thread.
- **Location**: Berlin, Germany
- **Website URL**: https://github.com/jo060235356-spec

---

## 2. GitLab Profile README.md (`username/username`)

```markdown
| [KR 한국어](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/ko.md) | [US English](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/README.md) | [JP 日本語](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/ja.md) | [CN 简体中文](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/zh-CN.md) | [ES Español](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/fr.md) | [DE Deutsch](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/de.md) | [RU Русский](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/ru.md) | [BR Português](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/pt-BR.md) | [SA العربية](https://github.com/jo060235356-spec/jo060235356-spec/blob/main/docs/locales/ar.md) |

---

# Julian Vance (j-vance)

> Audio DSP Systems Engineer & Real-Time Embedded Specialist  
> Berlin, Germany · Low-latency CI/CD pipelines, bare-metal audio builds, and deterministic signal processing.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ GitLab CI ] ---> [ Cross-Toolchains ] ---> [ Embedded Firmware / DSP ]
```

---

## 🧭 About & Focus on GitLab

Welcome to my GitLab hub. While my public open-source libraries live on GitHub, I use GitLab primarily for:
- Deterministic, multi-platform embedded firmware CI/CD pipelines (ARM Cortex-M7, RP2040).
- Continuous performance benchmarking of DSP hot-loops under strict timing constraints.
- Hardware-in-the-loop (HIL) testing for audio interfaces and custom board revisions.

---

## 🛠️ Systems & Toolchains Matrix

| Infrastructure & Embedded | Core Languages & Tools | Pipeline Focus |
| :--- | :--- | :--- |
| **Firmware CI/CD** | GitLab CI, Docker, CMake, Ninja | Reproducible cross-compilation for ARM-none-eabi, Clang/LLVM |
| **Sanitizers & Verification** | Clang ASan, UBSan, MSan | Zero-allocation auditing in audio callbacks, memory leak prevention |
| **Embedded Hardware** | STM32H7, RP2040, FreeRTOS | Bare-metal DMA audio streams, I2S bus validation |
| **Hardware-in-the-Loop** | Python, PyVISA, SCPI | Programmatic audio analyzer control, loopback latency testing |

---

## 🚀 Active GitLab Pipelines

- `dsp-benchmarks-runner`: Nightly performance regression testing on bare-metal Linux lowlatency kernels.
- `rp-mpe-firmware-ci`: Reproducible firmware artifact generation and DMA timing verification for RP2040 boards.
- `analog-wdf-sim`: Continuous Wave Digital Filter solver regression tests across AVX2 and ARM NEON targets.

---

## 📬 Contact

- GitHub: https://github.com/jo060235356-spec
- Email: `julian.vance.audio [at] proton.me`
- Matrix: `@jvance:matrix.org`

---

<sub>Zero allocations. Deterministic timing. Pure acoustics.</sub>
```
