| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Julian Vance (j-vance)

> Engenheiro de Sistemas DSP de Áudio & Entusiasta de Tempo Real de Ultra-Baixa Latência  
> Baseado em Berlim, Alemanha · Construindo pipelines determinísticos de DSP, plugins de áudio e firmware embarcado.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 Sobre Mim

Eu projeto, meço e otimizo sistemas de áudio digital em tempo real. Meu foco central está em pipelines de processamento de áudio com latência ultrabaixa, onde qualquer alocação dinâmica de memória na thread de renderização é terminantemente proibida e a precisão temporal determinística é inegociável.

- 🎛️ **Foco Principal**: Síntese por modelagem física em tempo real, emulação de topologias de filtros analógicos e kernels DSP acelerados por SIMD.
- ⚙️ **Engenharia de Hardware**: Áudio bare-metal embarcado em microcontroladores STM32H7 e Raspberry Pi RP2040.
- 📐 **Convicção Técnica**: Código livre de travas (lock-free) e com zero alocações no loop crítico (hot loop). Estouros e falhas de buffer (xruns) são bugs graves, não compromissos inevitáveis.
- ☕ **Vida Fora da Tela**: Colecionar gravadores de fita de rolo dos anos 1970, calibrar mecânicas de fita magnética e projetar pré-amplificadores analógicos discretos.

---

## 🛠️ Stack Tecnológico & Matriz de Domínios

### Sistemas Centrais & Processamento de Sinais
| Domínio | Linguagens & Ferramentas Principais | Áreas de Foco & Metodologias |
| :--- | :--- | :--- |
| **Sistemas de Tempo Real** | C++20/23, Rust, C99 | Atômicos lock-free, caminhos críticos sem alocação, alinhamento de cache |
| **DSP & Vetorização** | AVX2 / AVX-512, ARM NEON, FFTW3 | Cascatas biquad, Wave Digital Filters (WDF), oversampling polifásico |
| **Frameworks de Áudio** | JUCE 7/8, CLAP, VST3, WebAudio | Renderização customizada de GUI, suavização de parâmetros, modulação polifônica |
| **Embarcados & Hardware** | STM32 (ARM Cortex-M7), RP2040, KiCAD | Barramentos I2S/TDM, conversores DAC Cirrus Logic, esquemáticos de placas |
| **Análise & Modelagem** | Python, NumPy, SciPy, MATLAB | Modelagem de resposta em frequência, análise de resposta ao impulso, curvas SNR/THD |
| **Build & Toolchains** | CMake, Ninja, Cargo, LLVM/Clang | Sanitizadores rigorosos (`ASan`, `UBSan`), compilação cruzada determinística |

---

## 🚀 Principais Projetos de Código Aberto

### 1. `resonant-core` (C++20 / SIMD / CLAP)
Biblioteca modular de DSP de áudio em formato header-only voltada para processamento determinístico em tempo real.
- Implementa filtros de sobreamostragem polifásicos 4x/8x e topologias não-lineares de filtros ladder analógicos.
- Intrínsecos nativos AVX2 e ARM NEON com zero alocações de memória dentro dos blocos de processamento.
- Desempenho medido: 0,18 microssegundos por bloco de 64 amostras na arquitetura AMD Zen 4.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
Emulação em tempo contínuo da saturação magnética de fita e do flutter mecânico do eixo cabrestante.
- Modelagem física de histerese magnética utilizando resolvedores de equações diferenciais Runge-Kutta de 4ª ordem (RK4).
- Compilado para WebAssembly para demonstrações acústicas imediatas diretamente no navegador sem instalação.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
Firmware bare-metal de sintetizador para hardware customizado com suporte integral a Expressão Polifônica MIDI (MPE).
- Arquitetura dual-core: Core 0 dedicado ao processamento de pacotes USB/DIN-MIDI, Core 1 executando síntese subtrativa de 16 vozes a 48 kHz.
- Transmissão direta por DMA para DAC I2S estéreo de 24 bits sem a sobrecarga de um RTOS.

### 4. `ascii-spectrogram` (C99 / CLI Terminal)
Ferramenta de terminal de alta performance que renderiza espectrogramas de áudio em tempo real a 60 FPS com ANSI truecolor.
- Ring buffer livre de travas (lock-free) com conexão direta aos fluxos de áudio ALSA, PulseAudio, PipeWire e CoreAudio.
- Funções de janelamento (Hann, Blackman-Harris) computadas inteiramente por meio de instruções vetoriais SIMD.

---

## 📊 Registro de Benchmarks do Ambiente

```text
[BENCHMARKS ATUAIS DO AMBIENTE - 64 AMOSTRAS @ 96 kHz]
+-------------------------+----------------+----------------+------------+
| Módulo                  | Algoritmo      | Tempo de Loop  | Memória I/O|
+-------------------------+----------------+----------------+------------+
| Tape Hysteresis Sat     | RK4 / Non-lin  |   142 ns / ams |   0 alloc  |
| 4-Pole Moog Ladder WDF  | Trapezoidal    |    88 ns / ams |   0 alloc  |
| Polyphase Resampler 4x  | 64-tap Poly    |    34 ns / ams |   0 alloc  |
| Stereophonic Reverb     | FDN 16-channel |   210 ns / ams |   0 alloc  |
+-------------------------+----------------+----------------+------------+
* Medido utilizando LLVM 18 com -O3 -march=native no kernel Linux 6.8 lowlatency.
```

---

## 🤝 Colaboração & Contato

Estou sempre aberto a discussões sobre processamento digital de sinais, arquitetura de firmware embarcado, ajustes de kernel de baixa latência e prototipagem de hardware de áudio.

- 💬 **Tópicos que Adoro**: Estruturas de dados concorrentes lock-free, modelagem numérica de transistores discretos, acústica de salas, restauração de equipamentos de estúdio vintage.
- 📬 **Como me Encontrar**:
  - E-mail: `julian.vance.audio [at] proton.me`
  - Matrix: `@jvance:matrix.org`
  - GitHub Discussions: Fique à vontade para iniciar uma discussão em qualquer um dos meus repositórios.

---

<sub>Desenvolvido com genuína dedicação a código determinístico, matemática rigorosa e fidelidade acústica.</sub>
