# GoogleLyraCodec
Compiled Google Lyra codec binaries.

Google Lyra is a high-quality, low-bitrate speech codec that makes possible significantly better compression of audiobooks than MP3 and Ogg Vorbis.

Compiling source code (https://github.com/google/lyra, https://github.com/TFORevive/vaudio_lyra) using Bazel is a very challenging task. Both Bazel and the set of programs it uses are constantly evolving, and their versions are becoming incompatible with one another. After putting both myself and Google’s AI agent through the wringer numerous times, I decided to upload the binary versions of the files I needed to GitHub. Hopefully, having them available will make life easier and save time for anyone facing similar challenges.

The "vaudio_lyra_Windows" folder contains the binary files for Windows: vaudio_lyra.dll, decoder_main.exe, and encoder_main.exe from the "vaudio_lyra" project (https://github.com/TFORevive/vaudio_lyra). The file "lyravoicecodec.cc" contains the modified source code for the file https://github.com/TFORevive/vaudio_lyra/blob/main/vaudio_lyra/lyravoicecodec.cc.

The "Lyra_Android" folder contains the binary files for Android: decoder_main, encoder_main, liblyra_decoder.so, liblyra_encoder.so from the Google Lyra project (https://github.com/google/lyra).

Now, except the vaudio_lyra.dll, the Lyra codec **will not work** without its neural network model weights. Due to GitHub's file size limits and repository hygiene, you need to provide these files yourself:
1. Download the `.tflite` model files and configuration from the official repositories:
   * Standard models can be found in the Google Lyra Repository (https://github.com/google/lyra/tree/main/lyra/model_coeffs).
2. Create a folder named `model_coeffs` in the same directory as your executable.
3. Place the downloaded `.tflite` and `.proto` files into that `model_coeffs` folder.

Your local directory structure should look like this:
├── encoder_main.exe (or decoder_main)
└── model_coeffs/
    ├── lyra_config.proto
    ├── soundstream_encoder.tflite
    └── [other .tflite files...]
