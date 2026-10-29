| [KR 한국어](./ko.md) | [US English](../../README.md) | [JP 日本語](./ja.md) | [CN 简体中文](./zh-CN.md) | [ES Español](./es.md) |
| :---: | :---: | :---: | :---: | :---: |
| [FR Français](./fr.md) | [DE Deutsch](./de.md) | [RU Русский](./ru.md) | [SA العربية](./ar.md) | [IN हिन्दी](./hi.md) |

---

# Julian Vance (j-vance)

> Ingénieur Systèmes DSP Audio & Passionné de Temps Réel à Ultra-Basse Latence  
> Basé à Berlin, Allemagne · Développement de pipelines DSP déterministes, de plug-ins audio et de micrologiciels embarqués.

```text
       ___          _ _            ___  ____  ____  
      / _ \ _  _ __| (_)___       |   \/ ___||  _ \ 
     | (_) | || / _` | / _ \  _   | |) \___ \| |_) |
      \___/ \_,_\__,_|_\___/ (_)  |___/|____/| .__/ 
                                             |_|    
    [ SIMD ] <--- Lock-Free Ringbuffer ---> [ DAC 192kHz/32-bit ]
```

---

## 🧭 À Propos de Moi

Je conçois, mesure et optimise des systèmes audio numériques en temps réel. Mon travail se concentre sur les chaînes de traitement à très faible latence où toute allocation dynamique de mémoire dans le thread de rendu audio est formellement bannie et où la régularité temporelle n'est pas négociable.

- 🎛️ **Domaines de Prédilection** : Synthèse par modélisation physique en temps réel, émulation de topologies de filtres analogiques et noyaux DSP vectorisés via SIMD.
- ⚙️ **Ingénierie Matérielle** : Systèmes audio bare-metal sur microcontrôleurs STM32H7 et Raspberry Pi RP2040.
- 📐 **Conviction Technique** : Code sans verrou (lock-free) et sans aucune allocation dynamique dans la boucle critique (hot loop). Les désynchronisations de mémoire tampon (xruns) sont des anomalies majeures, jamais des compromis acceptables.
- ☕ **Hors Écran** : Restauration de magnétophones à bande des années 70, étalonnage de mécaniques à bobines libres et conception de préamplificateurs discrets analogiques.

---

## 🛠️ Stack Technique & Matrice de Compétences

### Systèmes Centraux & Traitement du Signal
| Domaine | Langages & Outils Principaux | Axes de Recherche & Méthodologies |
| :--- | :--- | :--- |
| **Systèmes Temps Réel** | C++20/23, Rust, C99 | Atomiques lock-free, chemins critiques sans allocation, alignement de lignes de cache |
| **DSP & Vectorisation** | AVX2 / AVX-512, ARM NEON, FFTW3 | Cascades biquad, filtres numériques d'onde (WDF), suréchantillonnage polyphase |
| **Frameworks de Plug-ins** | JUCE 7/8, CLAP, VST3, WebAudio | Moteur de rendu d'interface dédié, lissage de paramètres, modulation polyphonique |
| **Systèmes Embarqués** | STM32 (ARM Cortex-M7), RP2040, KiCAD | Bus I2S/TDM, convertisseurs DAC Cirrus Logic, conception de schémas électroniques |
| **Analyse & Simulation** | Python, NumPy, SciPy, MATLAB | Modélisation de réponse en fréquence, analyse de réponse impulsionnelle, mesures SNR/THD |
| **Chaînes de Compilation** | CMake, Ninja, Cargo, LLVM/Clang | Outils de diagnostic strict (`ASan`, `UBSan`), compilation croisée déterministe |

---

## 🚀 Principaux Projets Open-Source

### 1. `resonant-core` (C++20 / SIMD / CLAP)
Une bibliothèque DSP audio modulaire, sous forme d'en-têtes seuls (header-only), dédiée au traitement temps réel rigoureusement déterministe.
- Implémente des filtres de suréchantillonnage polyphases 4x/8x et des topologies non linéaires de filtres en échelle analogiques.
- Accélération native par intrinsèques AVX2 et ARM NEON, sans aucune allocation mémoire au sein des blocs de calcul.
- Mesure de performance : 0,18 microseconde par bloc de 64 échantillons sur microarchitecture AMD Zen 4.

### 2. `reel-flutter` (Rust / WebAssembly / VST3)
Émulation en temps continu de la saturation magnétique de bande et du scintillement mécanique de cabestan (pleurage et scintillement).
- Modélisation physique de l'hystérésis magnétique via des solveurs d'équations différentielles de Runge-Kutta d'ordre 4 (RK4).
- Compilé vers WebAssembly pour permettre une évaluation acoustique instantanée dans le navigateur, sans installation.

### 3. `rp-mpe-engine` (Embedded Rust / RP2040)
Micrologiciel bare-metal de synthétiseur pour plateforme matérielle sur mesure avec support intégral de l'expression polyphonique MIDI (MPE).
- Architecture à double cœur : le Cœur 0 prend en charge l'analyse des paquets USB/DIN-MIDI, le Cœur 1 exécute le moteur soustractif 16 voix à 48 kHz.
- Flux DMA direct alimentant un DAC I2S stéréo 24 bits sans l'empreinte d'un RTOS.

### 4. `ascii-spectrogram` (C99 / CLI Terminal)
Outil en ligne de commande affichant un spectrogramme audio fluide à 60 FPS en couleurs vraies ANSI au sein du terminal.
- Búfer circulaire lock-free directement interfacé avec les flux audio ALSA, PulseAudio, PipeWire et CoreAudio.
- Fonctions de fenêtrage (Hann, Blackman-Harris) entièrement vectorisées par instructions SIMD.

---

## 📊 Relevé des Bancs d'Essai Techniques

```text
[BENCHMARKS DE L'ENVIRONNEMENT DE TRAVAIL - 64 ÉCHANTILLONS @ 96 kHz]
+-------------------------+----------------+----------------+------------+
| Module                  | Algorithme     | Temps Boucle   | E/S Mémoire|
+-------------------------+----------------+----------------+------------+
| Tape Hysteresis Sat     | RK4 / Non-lin  |   142 ns / ech |   0 alloc  |
| 4-Pole Moog Ladder WDF  | Trapezoidal    |    88 ns / ech |   0 alloc  |
| Polyphase Resampler 4x  | 64-tap Poly    |    34 ns / ech |   0 alloc  |
| Stereophonic Reverb     | FDN 16-channel |   210 ns / ech |   0 alloc  |
+-------------------------+----------------+----------------+------------+
* Mesuré avec LLVM 18 (-O3 -march=native) sur noyau Linux 6.8 lowlatency.
```

---

## 🤝 Échanges & Contact

Je suis toujours ravi d'échanger sur le traitement du signal numérique, l'architecture logicielle embarquée, la configuration de noyaux à faible latence et le prototypage d'instruments électroniques.

- 💬 **Sujets Favoris** : Structures de données concurrentes lock-free, modélisation de semi-conducteurs discrets, acoustique des salles, restauration de circuits audio vintage.
- 📬 **Me Contacter** :
  - E-mail : `julian.vance.audio [at] proton.me`
  - Matrix : `@jvance:matrix.org`
  - Discussions GitHub : Vous êtes les bienvenus pour ouvrir un fil d'échange sur mes dépôts.

---

<sub>Élaboré avec une passion authentique pour le code déterministe, les mathématiques pures et la fidélité acoustique.</sub>
