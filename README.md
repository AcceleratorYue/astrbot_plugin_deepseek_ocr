# DeepSeek OCR · `astrbot_plugin_deepseek_ocr`

> AstrBot 插件 · 版本 `0.1.1` · 作者 AcceleratorYue · MIT License  
> 仓库：<https://github.com/AcceleratorYue/astrbot_plugin_deepseek_ocr>  
> 兼容：AstrBot `>=4.16,<5`，平台 `aiocqhttp`（NapCat / OneBot v11）

用 DeepSeek OCR 识别群聊/私聊中的图片、PDF、Word、PPT 文字，并作为临时资料交给主模型。

## 安装

### 插件市场

在 AstrBot WebUI →「插件」→「插件市场」搜索 **DeepSeek OCR**。

### GitHub

```bash
cd <AstrBot根目录>/data/plugins
git clone https://github.com/AcceleratorYue/astrbot_plugin_deepseek_ocr
```

### 手动安装

把本目录复制到：

```text
<AstrBot根目录>/data/plugins/astrbot_plugin_deepseek_ocr
```

然后在 AstrBot WebUI →「插件管理」重载插件，或重启 AstrBot。

## 正确触发方式

QQ 里不能在“发送文件”的同一条消息里再 @Bot。实际操作方式是：

1. 先发送图片 / PDF / Word / PPT；
2. **引用（回复）这条带附件的消息**，输入 `@Bot` 加你的问题；
3. 插件会读取引用消息里的附件并 OCR，再把文字交给模型回答。

也可以引用附件消息后直接发送：

```text
/ocr
```

## 功能

- 引用带图片/文档的消息并 `@Bot` 时，自动 OCR 后注入当前 LLM 请求；
- 支持先发附件、再引用后 @Bot 提问（默认 600 秒内复用最近结果）；
- `/ocr`：识别当前消息或引用消息中的附件；
- 按文件哈希缓存，避免同一附件反复调用；
- OCR 内容标记为临时资料，不写入长期对话历史；
- 未配置 `api_key` 时自动复用 AstrBot 已配置的 DeepSeek Key。

## 配置

主要配置：

```text
enable                 启用插件
auto_inject            自动识别并注入
reuse_seconds          最近结果复用时间
purpose                text_recognition / rich_layout_recognition
max_files_per_message  单条消息最多几个附件
max_file_mb            单文件大小上限
max_injected_chars     注入上下文的最大字符数
```

`purpose=text_recognition` 成本低，适合文字截图；`rich_layout_recognition` 保留版面/图片位置，适合带图表的文档，但输入 Token 更多。

## 限制

- 只识别文字，不替代视觉模型理解图片内容；
- OCR 可能有错字、漏字、版面顺序问题；
- DeepSeek 官方限制：单文件 100 MiB、最多 1000 页、整体最长 180 秒；
- 纯文本文件（`.txt/.md/.log` 等）建议交给文本文件读取插件，不走 OCR。

## 手动测试

```text
/ocr
```

或引用一条带图片/文件的消息后发送 `/ocr`。

## 许可证

MIT License，详见 [LICENSE](LICENSE)。
