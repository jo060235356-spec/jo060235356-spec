| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Julian Vance (j-vance)

> Senior Audio-DSP- und Systemingenieur & Enthusiast für deterministische Echtzeit-Niedrigstlatenz  
> Ansässig in Berlin, Deutschland · Entwicklung von DSP-Pipelines, Audio-Plugins und Embedded-Firmware.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 Über Mich

Ich entwerfe, messe und optimiere digitale Echtzeit-Audiosysteme. Mein Schwerpunkt liegt auf extrem latenzarmen Signalverarbeitungsketten, bei denen dynamische Speicherallokationen im Audio-Render-Thread strikt untersagt sind und deterministisches Zeitverhalten oberste Priorität hat.

- 🎛️ **Fachliche Schwerpunkte**: Echtzeit-Synthese durch physikalische Modellierung, Emulation analoger Filtertopologien und SIMD-optimierte DSP-Kernel.
- ⚙️ **Hardware-Entwicklung**: Bare-Metal-Audioverarbeitung auf STM32H7- und Raspberry Pi RP2040-Mikrocontrollern.
- 📐 **Ingenieurphilosophie**: Sperrfreie (lock-free) Algorithmen und null Speicherallokationen im kritischen Ausführungspfad (Hot Loop). Audio-Pufferunterläufe (xruns) sind handfeste Bugs, keine unvermeidbaren Kompromisse.
- ☕ **Abseits des Bildschirms**: Sammeln von Tonbandmaschinen der 1970er Jahre, Justierung von Bandmechaniken und Entwurf diskreter analoger Vorverstärkerstufen.

---

## 🛠️ Technologie-Stack & Domänen-Matrix

### Kernsysteme & Signalverarbeitung
| Fachbereich | Primäre Sprachen & Werkzeuge | Schwerpunkte & Methodik |
| :--- | :--- | :--- |
| **Echtzeitsysteme** | C++20/23, Rust, C99 | Sperrfreie Atomics, allokationsfreie Signalpfade, Cache-Line-Ausrichtung |
| **DSP & Vektorisierung** | AVX2 / AVX-512, ARM NEON, FFTW3 | Biquad-Kaskaden, Wave-Digital-Filter (WDF), Polyphasen-Oversampling |
| **Plugin-Frameworks** | JUCE 7/8, CLAP, VST3, WebAudio | Eigenentwickelte GUI-Pipelines, Parameter-Glättung, polyphone Modulation |
| **Embedded & Hardware** | STM32 (ARM Cortex-M7), RP2040, KiCAD | I2S/TDM-Busanbindung, Cirrus Logic DAC-Treiber, Leiterplatten-Entwurf |
| **Messung & Modellierung** | Python, NumPy, SciPy, MATLAB | Frequenzgangmodellierung, Impulsantwortanalysen, THD- und SNR-Sweeps |
| **Build-Systeme** | CMake, Ninja, Cargo, LLVM/Clang | Strikte Sanitizer (`ASan`, `UBSan`), reproduzierbare Cross-Kompilierung |

---

## 🚀 Wichtige Open-Source-Projekte

### 1. `resonant-core` (C++20 / SIMD / CLAP)
Eine modulare, reine Header-DSP-Bibliothek für deterministische Echtzeitverarbeitung.
- Implementierung von 4x/8x-Polyphasen-Oversamplingfiltern und nichtlinearen Transistor-Kaskadenfiltern.
- Native AVX2- und ARM NEON-Intrinsics ohne jede dynamische Speicherallokation innerhalb der Verarbeitungsblöcke.
- Benchmark: 0,18 Mikrosekunden pro 64-Sample-Block auf AMD Zen 4-Architektur.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
Kontinuierliche mathematische Modellierung von magnetischer Bandsättigung und mechanischem Gleichlauffehler (Flutter).
- Simulation von magnetischer Hysterese mittels Runge-Kutta-Differentialgleichungslösern 4. Ordnung (RK4).
- Kompiliert nach WebAssembly für sofortige akustische Demonstrationen direkt im Webbrowser ohne Installation.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
Bare-Metal-Synthesizer-Firmware für maßgeschneiderte Audiohardware mit nativer MIDI-Polyphonic-Expression (MPE).
- Zweikern-Aufteilung: Core 0 übernimmt USB/DIN-MIDI-Parsing, Core 1 berechnet eine subtraktive Synthese mit 16 Stimmen bei 48 kHz.
- Direkte DMA-Pufferübertragung an einen 24-Bit-Stereo-I2S-DAC völlig ohne RTOS-Overhead.

### 4. `ascii-spectrogram` (C99 / Terminal-CLI)
Ein performantes Terminal-Werkzeug, das Echtzeit-Audio-Spektrogramme mit 60 FPS in ANSI-Truecolor rendert.
- Sperrfreier Ringpuffer mit direkter Anbindung an ALSA-, PulseAudio-, PipeWire- und CoreAudio-Datenströme.
- Fensterungsfunktionen (Hann, Blackman-Harris) vollständig über SIMD-Vektorbefehle optimiert.

---

## 📊 Aktuelle Benchmark-Ergebnisse

```text
[SYSTEM-MESSUNGEN ARBEITSPLATZ - 64 SAMPLES @ 96 kHz]
+-------------------------+----------------+----------------+------------+
| Modul                   | Algorithmus    | Rechenzeit     | Speicher   |
+-------------------------+----------------+----------------+------------+
| Tape Hysteresis Sat     | RK4 / Non-lin  |   142 ns / smp |   0 alloc  |
| 4-Pole Moog Ladder WDF  | Trapezoidal    |    88 ns / smp |   0 alloc  |
| Polyphase Resampler 4x  | 64-tap Poly    |    34 ns / smp |   0 alloc  |
| Stereophonic Reverb     | FDN 16-channel |   210 ns / smp |   0 alloc  |
+-------------------------+----------------+----------------+------------+
* Gemessen mit LLVM 18 (-O3 -march=native) auf Linux 6.8 Lowlatency-Kernel.
```

---

## 🤝 Kooperation & Austausch

Ich stehe fachlichen Diskussionen über digitale Signalverarbeitung, Embedded-Firmware-Architektur, Latenzoptimierung auf Betriebssystemebene und analoge Audio-Hardware stets aufgeschlossen gegenüber.

- 💬 **Themen, die mich begeistern**: Sperrfreie Datenstrukturen, diskrete Halbleitermodellierung, Raumakustik, Restaurierung klassischer Tonstudiogeräte.
- 📬 **Kontaktmöglichkeiten**:
  - E-Mail: `julian.vance.audio [at] proton.me`
  - Matrix: `@jvance:matrix.org`
  - GitHub Discussions: Tausche dich gerne direkt in den jeweiligen Repositorien mit mir aus.

---

<sub>Geschrieben mit authentischer Hingabe für deterministischen Code, mathematische Exaktheit und reine Akustik.</sub>
