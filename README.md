# Offline Chinese–English translator for Scoreler

A CPU-only sentence translator using bundled neural machine translation models. After installing the release ZIP, it needs no internet, account, ChatGPT plan, API key or separate model download.

## Use

1. Update Scoreler to **1.3.2 or later** (plugin format v2).
2. Open Toolbox / 百宝箱 → Plugins / 插件, review and install **Offline Chinese–English translator**. The download includes both models and is much larger than a calculator plugin.
3. Open its card directly in Toolbox. Choose automatic detection, English → Simplified Chinese, or Chinese → English. Type or paste text and select Translate.
4. Select translation and press Ctrl+C to copy using the normal keyboard action. Swap places the output in the input field and reverses the direction.

Text and translations remain in the isolated tool. Nothing is sent to a service. No history is saved, and leaving the tool discards its state. Only CPU WebAssembly is used; no CUDA, RTX or GPU inference is enabled. The first translation loads one bundled model into memory. Switching directions disposes the previous model.

Up to 2,000 characters per request. Input is split into short sentences/chunks to fit the compact model. Stop takes effect after the current sentence. This older compact translation model can mistranslate names, specialist terms, idioms and ambiguous text. It is not a certified translator, and important output needs human review. Long documents and document attachments are not supported.

## Open-source credits and licences

- **OPUS-MT**, Language Technology Research Group, University of Helsinki. Jörg Tiedemann and Santhosh Thottingal, *OPUS-MT: Building open translation services for the World* (EAMT 2020).
- [English → Chinese model](https://huggingface.co/Helsinki-NLP/opus-mt-en-zh): **Apache-2.0**.
- [Chinese → English model](https://huggingface.co/Helsinki-NLP/opus-mt-zh-en): **CC-BY-4.0**.
- [Xenova English → Chinese](https://huggingface.co/Xenova/opus-mt-en-zh) and [Xenova Chinese → English](https://huggingface.co/Xenova/opus-mt-zh-en): upstream ONNX conversion and INT8 quantization. Bundled files are unchanged from the pinned revisions. The conversions retain the original model licences and attribution.
- [Transformers.js](https://github.com/huggingface/transformers.js), version 2.17.2: Apache-2.0, Hugging Face / Xenova and contributors.
- [ONNX Runtime](https://github.com/microsoft/onnxruntime), version 1.14.0: MIT, Microsoft Corporation.
- Plugin interface, offline asset adapter and build scripts: MIT, Scoreler contributors. These are the Scoreler-specific adaptations, not changes to the upstream model weights.

The package LICENSE includes the full licence texts. Credits are also visible in the tool. No endorsement by the upstream authors is claimed. Model revisions, upstream hashes and local SHA-256 hashes are recorded in upstream.lock.json and models.lock.json.

## Reproduce

Use Node.js 24 or later. Run `npm ci --ignore-scripts`, `node download-models.cjs`, then `node build.cjs`. Build-time downloads use HTTPS and verify pinned upstream Git/LFS hashes. An optional `SCORELER_BUILD_PROXY` environment variable can route build downloads through your own proxy; no address is saved in the source. Runtime network access stays blocked.

Build output is `dist/offline-translator-1.0.0.zip`. Model downloads, node_modules, generated HTML and ZIP files are excluded from Git; models are distributed only inside the release ZIP. `npm ci --ignore-scripts` avoids native image-library install scripts; this plugin uses the prebuilt browser-only Transformers.js bundle.

## 中文

这是完全离线的中英双向短句翻译插件。安装包自带两个量化 OPUS-MT 神经翻译模型，在本机 CPU 上运行；安装后无需联网、账号、API 密钥或额外下载模型。需要 Scoreler 1.3.2 或更新版本，在百宝箱 → 插件中安装，然后直接点击百宝箱中的卡片使用。

支持自动检测、英文译简体中文、中文译英文、交换输入输出、选择译文。每次最多 2,000 字符，长内容按短句分段处理。首次加载与翻译速度取决于 CPU 和内存。当前句完成后可停止后续翻译。离开工具后不保存输入、译文或历史。

小型旧模型可能误译专业词汇、人名、习语和歧义表达，重要内容请人工核对。上方列明了 OPUS-MT、Xenova、Transformers.js 和 ONNX Runtime 的完整来源与许可；工具内也有可见致谢。中译英模型为 CC-BY-4.0，英译中模型为 Apache-2.0，插件自身代码为 MIT。
