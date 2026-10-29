# Hugging Face Profile Specification: Julian Vance

## 1. Account Settings (Settings -> Profile)

- **Full Name**: Julian Vance
- **Bio**: Audio DSP & low-latency systems engineer. Exploring Differentiable Digital Signal Processing (DDSP), neural audio codecs, and physical modeling datasets. Focused on real-time deterministic inferencing on edge DSPs and embedded targets.
- **GitHub Username**: jo060235356-spec
- **Homepage / Website**: https://github.com/jo060235356-spec
- **Interests**: `audio-dsp`, `differentiable-dsp`, `neural-audio-codecs`, `embedded-inference`, `acoustics`

---

## 2. Profile Overview & Repository Orientations

### 🧭 Research Direction & Focus

My work bridges classical continuous-time digital signal processing (DSP) and differentiable physical modeling. Rather than building massive black-box generative models, I focus on:
1. **Ultra-Compact Neural Audio Models**: Micro-architectures designed for real-time execution inside audio plugin threads (< 1.5 ms buffer budgets).
2. **Deterministic ONNX / C++ Pipelines**: Exporting models to ONNX and compiling directly into bare-metal C++20 and SIMD kernels.
3. **High-Fidelity Acoustic Datasets**: Precision impulse responses and non-linear saturation profiles captured from discrete analog hardware and vintage magnetic tape machines.

---

### 📦 Key Models & Directions

| Model Category | Architecture / Tech | Target Application |
| :--- | :--- | :--- |
| **`ddsp-analog-ladder`** | Differentiable WDF / PyTorch | Differentiable non-linear 4-pole ladder filter for real-time parameter tracking |
| **`tape-hysteresis-net`** | Tiny GRU (8-hidden) / ONNX | Continuous-time tape core saturation emulation running under 60 microseconds per block |
| **`fast-codec-quantized`** | Neural Audio Codec / INT8 | Low-bitrate streaming codec optimized for microcontrollers with SIMD support |

---

### 🗄️ Acoustic & Measurement Datasets

- **`studer-a80-saturation-sweep`**: 96 kHz / 24-bit multi-level saturation and dynamic frequency response sweeps across 3M 996 and Ampex 456 tape formulations.
- **`discrete-germanium-preamp-ir`**: High-resolution non-linear impulse response collection capturing harmonic distortion profiles of vintage germanium transistor stages.
- **`acoustic-chamber-decay-64ch`**: 64-channel spatial impulse response library for calibrating feedback delay networks (FDN) and wave field synthesis.

---

### 🧪 Interactive Spaces

- **`tape-flutter-wasm-demo`**: Interactive in-browser demo simulating physical capstan flutter and magnetic tape compression in real time using WebAssembly and WebAudio.
- **`wdf-filter-inspector`**: Interactive visualization comparing frequency and phase responses between classical Wave Digital Filters and neural approximations.

---

<sub>Dedicated to deterministic code, clean mathematics, and pure acoustics.</sub>
