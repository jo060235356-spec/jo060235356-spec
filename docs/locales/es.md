| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Julian Vance (j-vance)

> Ingeniero de Sistemas DSP de Audio & Entusiasta del Tiempo Real de Ultra-Baja Latencia  
> Con base en Berlín, Alemania · Desarrollando pipelines DSP deterministas, plugins de audio y firmware embebido.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 Sobre Mí

Diseño, mido y optimizo sistemas de audio digital en tiempo real. Mi enfoque principal radica en los pipelines de procesamiento de baja latencia donde las asignaciones dinámicas de memoria en el hilo de renderizado están terminantemente prohibidas y la precisión temporal determinista no es negociable.

- 🎛️ **Enfoque Principal**: Síntesis por modelado físico en tiempo real, emulación de topologías de filtros analógicos y kernels DSP acelerados por SIMD.
- ⚙️ **Ingeniería de Hardware**: Audio bare-metal embebido en microcontroladores STM32H7 y Raspberry Pi RP2040.
- 📐 **Filosofía Técnica**: Código sin bloqueos (lock-free) y con cero asignaciones dinámicas en el bucle crítico (hot loop). Las caídas de búfer de audio (xruns) son errores graves, nunca compromisos inevitables.
- ☕ **Vida Desconectada**: Coleccionar grabadoras de cinta de bobina abierta de los años 70, calibrar mecánicas de cinta y diseñar preamplificadores analógicos discretos.

---

## 🛠️ Stack Tecnológico & Matriz de Dominios

### Sistemas Centrales & Procesamiento de Señales
| Dominio | Herramientas & Lenguajes Clave | Áreas de Enfoque & Metodologías |
| :--- | :--- | :--- |
| **Sistemas en Tiempo Real** | C++20/23, Rust, C99 | Atómicas lock-free, rutas críticas sin asignación, alineación de caché |
| **DSP & Vectorización** | AVX2 / AVX-512, ARM NEON, FFTW3 | Cascadas biquad, Wave Digital Filters (WDF), filtros polifásicos |
| **Frameworks de Audio** | JUCE 7/8, CLAP, VST3, WebAudio | Renderizado de GUI personalizado, suavizado de parámetros, modulación polifónica |
| **Embebido & Hardware** | STM32 (ARM Cortex-M7), RP2040, KiCAD | Buses I2S/TDM, convertidores DAC Cirrus Logic, diseño de esquemáticos PCB |
| **Análisis & Simulación** | Python, NumPy, SciPy, MATLAB | Modelado de respuesta en frecuencia, análisis de respuesta al impulso, curvas SNR/THD |
| **Compilación & Toolchains** | CMake, Ninja, Cargo, LLVM/Clang | Sanitizadores estrictos (`ASan`, `UBSan`), compilación cruzada determinista |

---

## 🚀 Proyectos Destacados de Código Abierto

### 1. `resonant-core` (C++20 / SIMD / CLAP)
Biblioteca modular de DSP de audio de solo encabezados (header-only) diseñada para procesamiento determinista en tiempo real.
- Implementa filtros de sobremuestreo polifásicos 4x/8x y topologías no lineales de filtros escalera analógicos.
- Intrínsecos nativos AVX2 y ARM NEON con cero asignaciones de memoria dentro de los bloques de procesamiento.
- Rendimiento medido: 0.18 microsegundos por bloque de 64 muestras en arquitectura AMD Zen 4.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
Emulación en tiempo continuo de la saturación magnética de cinta y el lloro/fluctuación (flutter) mecánico del cabrestante.
- Modelado físico de histéresis magnética mediante solucionadores de ecuaciones diferenciales Runge-Kutta de 4º orden (RK4).
- Compilado a WebAssembly para pruebas acústicas inmediatas directamente en el navegador sin instalación.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
Firmware bare-metal de sintetizador para hardware a medida con soporte completo de Expresión Polifónica MIDI (MPE).
- Arquitectura de doble núcleo: Núcleo 0 dedicado al procesamiento de paquetes USB/DIN-MIDI; Núcleo 1 ejecutando un motor sustractivo de 16 voces a 48 kHz.
- Transmisión directa por DMA a un DAC I2S estéreo de 24 bits sin sobrecarga de RTOS.

### 4. `ascii-spectrogram` (C99 / CLI de Terminal)
Herramienta de línea de comandos de alto rendimiento que renderiza espectrogramas de audio en cascada a 60 FPS en color verdadero ANSI.
- Búfer circular sin bloqueos (lock-free ringbuffer) conectado directamente a flujos de ALSA, PulseAudio, PipeWire y CoreAudio.
- Funciones de ventanéo (Hann, Blackman-Harris) calculadas íntegramente mediante instrucciones vectoriales SIMD.

---

## 📊 Registro de Benchmarks del Entorno de Trabajo

```text
[BENCHMARKS ACTUALES DE TRABAJO - 64 MUESTRAS @ 96 kHz]
+-------------------------+----------------+----------------+------------+
| Módulo                  | Algoritmo      | Tiempo Hot-Loop| Memoria I/O|
+-------------------------+----------------+----------------+------------+
| Tape Hysteresis Sat     | RK4 / Non-lin  |   142 ns / smp |   0 alloc  |
| 4-Pole Moog Ladder WDF  | Trapezoidal    |    88 ns / smp |   0 alloc  |
| Polyphase Resampler 4x  | 64-tap Poly    |    34 ns / smp |   0 alloc  |
| Stereophonic Reverb     | FDN 16-channel |   210 ns / smp |   0 alloc  |
+-------------------------+----------------+----------------+------------+
* Medido utilizando LLVM 18 con -O3 -march=native en kernel Linux 6.8 lowlatency.
```

---

## 🤝 Colaboración & Contacto

Siempre estoy disponible para debatir sobre procesamiento digital de señales, arquitectura de firmware embebido, afinación de kernels de baja latencia y prototipado de hardware de audio.

- 💬 **Temas que me apasionan**: Estructuras de datos concurrentes lock-free, modelado numérico de transistores discretos, acústica de salas, restauración de electrónica vintage.
- 📬 **Medios de Contacto**:
  - Correo: `julian.vance.audio [at] proton.me`
  - Matrix: `@jvance:matrix.org`
  - GitHub Discussions: Cualquier hilo en mis repositorios es bienvenido.

---

<sub>Desarrollado con auténtica devoción por el código determinista, las matemáticas rigurosas y la pureza acústica.</sub>
