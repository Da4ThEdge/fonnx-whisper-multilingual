# FONNX modified for multilingual Whisper models 

### ℹ️ This is a modified version of the original [FONNX library by Telosnex](https://github.com/Telosnex/fonnx), to make it accept `decoder_input_ids`, required by multilingual Whisper models exported via [Microsoft's Olive Toolchain](https://github.com/microsoft/Olive/tree/6ab9d8bb9284a89ccc87c63ca323c0f3386f6426).

👉 `decoder_input_ids` is used to force-set the `task`, `language` and whether `timestamps` will be generated or not for multilingual Whisper models.

👉 Here `decoder_input_ids` are currently set to `[ 50258, 50302, 50359, 50363 ]` for Bengali Transcription task:
- `"<|startoftranscript|>": 50258`
- `task: transcribe` ➡️ `"<|transcribe|>": 50359`
- `language: Bengali` ➡️ `"<|bn|>": 50302`
- `"<|notimestamps|>": 50363`

🤗 List of all tokens for any Huggingface Whisper Models can be found at [added_tokens.json](https://huggingface.co/openai/whisper-small/resolve/main/added_tokens.json)

👉 Changes are made to the following 4 files, where mainly `logits_processor` is being replaced by `decoder_input_ids`:
- OrtWhisper.kt `android\src\main\kotlin\com\telosnex\fonnx\OrtWhisper.kt`
- OrtWhisper.swift `ios\Classes\OrtWhisper.swift`
- fonnx_whisper_worker.js `docs\fonnx_whisper_worker.js`
- whisper_isolate.dart `lib\models\whisper\whisper_isolate.dart`

### 📱 Here's a [demo Flutter app](https://github.com/Da4ThEdge/banglabridge) using this modified FONNX package for Bengali Speech Transcription.