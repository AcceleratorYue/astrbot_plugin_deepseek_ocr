# Changelog

## 0.1.1 (2026-11-21)

首次开源发布。

- 支持引用消息中的图片、PDF、Word、PPT OCR；
- OCR 结果作为临时资料注入当前 LLM 请求，不写入长期历史；
- 支持 `/ocr` 手动识别和按文件哈希缓存；
- 未配置 API Key 时复用 AstrBot 的 DeepSeek Provider。
