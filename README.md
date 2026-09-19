# Google Lyra Precompiled Codec Binaries

[![Platform: Windows](https://img.shields.io/badge/Platform-Windows-0078D6?style=flat&logo=windows&logoColor=white)](https://github.com/AudioBookTech/GoogleLyraCodec)
[![Platform: Android](https://img.shields.io/badge/Platform-Android-3DDC84?style=flat&logo=android&logoColor=white)](https://github.com/AudioBookTech/GoogleLyraCodec)
[![Arch](https://img.shields.io/badge/Arch-x64_%7C_ARM64-lightgrey.svg)](https://github.com/AudioBookTech/GoogleLyraCodec)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

A curated collection of verified, ready-to-use precompiled binaries and libraries for the **Google Lyra** neural speech codec, targeting both **Windows** and **Android** platforms.

Google Lyra is a breakthrough, AI-driven speech codec engineered for ultra-low bitrate audio transmission. It enables orders-of-magnitude higher compression ratios for spoken word and audiobooks compared to legacy codecs such as MP3 or Ogg Vorbis, while preserving natural speech clarity and intelligibility.

---

## 💡 Why This Repository Exists

Compiling Google Lyra and its native derivatives directly from source (such as [google/lyra](https://github.com/google/lyra) or [TFORevive/vaudio_lyra](https://github.com/TFORevive/vaudio_lyra)) is an extraordinarily complex engineering hurdle. 

The native build pipeline relies on complex Bazel workspace structures and tightly coupled dependencies (TensorFlow Lite, Abseil, FlatBuffers, Protobuf) that frequently experience version drift and upstream toolchain bitrot. After extensive testing, debugging, and iterative builds conducted in close collaboration with Google AI, these prebuilt binaries were produced to remove the compilation barrier and save developers countless hours of setup.

---

## 🌟 The "Powered by Google Lyra" Ecosystem

This binary distribution is an integral asset for the **Powered by Google Lyra** family of audio tools:

* 🎛️ **[LyraCodec](https://apps.microsoft.com/detail/9mz8kt923n6l?hl=en-US&gl=US)** — A modern Windows utility for ultra-low-bitrate audio encoding and decoding.
* 📖 **[Ulenspigel](https://github.com/AudioBookTech/Ulenspigel)** — A standalone open-source Android [audiobook player](https://play.google.com/store/apps/details?id=com.KonstantinShramko.Ulenspigel) built on Lyra.
* 📚 **[Lyra Books](https://play.google.com/store/apps/details?id=com.KonstantinShramko.LyraBooks)** — An audiobook library launcher designed to organize Lyra-based book applications.
* 🛠️ **[Lyra Android Decoder (Bazel 9.2.0 + NDK r29)](https://github.com/AudioBookTech/LyraAndroid)** — Modern source-level build pipeline and JNI wrapper for Android arm64-v8a.
* 📖 **[LyraAndroid Wiki](https://github.com/AudioBookTech/LyraAndroid/wiki)** — Comprehensive guides, encoding parameters, and architecture documentation.

---

## 📁 Repository Structure & Contents

    GoogleLyraCodec/
    ├── vaudio_lyra_Windows/      # Windows x64 binaries, DLLs, and usage scripts
    ├── vaudio_lyra_Android/      # Android x64 shared libraries (.so)
    ├── Lyra_Android/             # Native Android executables and shared libraries
    ├── lyravoicecodec.cc         # Patched C++ source code for vaudio_lyra integration
    ├── encode_example.cmd        # Command-line batch example for encoding
    └── decode_example.cmd        # Command-line batch example for decoding

---

### 1. `vaudio_lyra_Windows/`
Windows binaries built from the [vaudio_lyra](https://github.com/TFORevive/vaudio_lyra) project:
* `vaudio_lyra.dll` — Dynamic-link library for runtime integration.
* `encoder_main.exe` — Standalone command-line audio encoder.
* `decoder_main.exe` — Standalone command-line audio decoder.
* `encode_example.cmd` & `decode_example.cmd` — Quick-start scripts demonstrating proper parameter flags for command-line encoding and decoding.
* `lyravoicecodec.cc` — Contains modified source code addressing build and runtime compatibility for `vaudio_lyra`.

### 2. `vaudio_lyra_Android/`
Prebuilt native Android x64 shared libraries:
* `liblyra_encoder.so` — Native encoder library.
* `liblyra_decoder.so` — Native decoder library.

### 3. `Lyra_Android/`
Binaries compiled directly against upstream Google Lyra:
* `encoder_main` — Command-line Android encoder binary.
* `decoder_main` — Command-line Android decoder binary.
* `liblyra_encoder.so` — Shared library for Android integration.
* `liblyra_decoder.so` — Shared library for Android integration.

---

## 🧠 Neural Network Model Weights (`model_coeffs`)

Please note that the upstream binaries in the `Lyra_Android/` folder **require access to the neural network model weights** to initialize at runtime. Due to repository size hygiene, binary weight models are not duplicated in this repo:

1. Download the `model_coeffs` directory containing the `.tflite` model files directly from the [Official Google Lyra Repository](https://github.com/google/lyra/tree/main/lyra/model_coeffs).
2. Place the downloaded `model_coeffs` folder in the same execution directory alongside the binary or library before running.

*(Note: If you need an Android decoder with models embedded directly into the binary without requiring external `.tflite` files, see our [Lyra Android Decoder](https://github.com/AudioBookTech/LyraAndroid) project).*

---

## 🚀 Usage Examples

### Windows Audio Encoding
Execute `encode_example.cmd` or run directly from the command prompt:

    encoder_main.exe --input_path="input.wav" --output_path="output.lyra" --bitrate=3200

### Windows Audio Decoding
Execute `decode_example.cmd` or run directly from the command prompt:

    decoder_main.exe --encoded_path="input.lyra" --output_path="decoded.wav"

---

## 🤝 Acknowledgments
Overcoming the intricate toolchain, dependency, and compilation challenges of Bazel would not have been possible without the tireless assistance, patience, and guidance of **Google AI**.  

Dedicated to all developers building next-generation audio applications: may these prebuilt binaries save you precious time and effort!

---

## 📄 License

This repository and auxiliary scripts are distributed under the **GNU General Public License v3.0** (GPL-3.0). See the [LICENSE](LICENSE) file for details.  
Precompiled components and algorithms derived from Google Lyra are subject to the original [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

