# 一次性 LLM 对话（chat.py）开发提示词

请用 Python 编写一个单文件命令行程序 `chat.py`，实现一次性 LLM 单轮对话，要求如下：

1. **配置文件**：在同目录生成 `config.ini`，内容如下（三个字段名固定）：

```ini
[llm]
base_url = https://你的接口地址/v1
api_key = 你的key
model = 你的模型名
```

程序用 `configparser` 读取这三个值。

2. **依赖与调用**：仅使用 `requests`（不引入 openai SDK）。调用 OpenAI 兼容的 `POST {base_url}/chat/completions` 接口：请求头 `Authorization: Bearer {api_key}`，请求体包含 `model` 和 `messages`（一条 system 提示 + 一条用户问题）。

3. **交互流程**（用户运行 `python chat.py` 后）：
   - 先打印欢迎语（如：你好，请提出你的问题）
   - 读取用户输入的一行问题
   - 打印 `……`（表示 AI 思考中）
   - 调用接口发送该问题
   - 打印 AI 返回的 `content` 回复
   - 程序退出（一次性对话，不保存历史、不继续多轮）

4. **简洁优先**：不做冗余设计。仅加基本的 `try/except` 捕获网络或接口错误并打印错误信息，不要加重试、日志、命令行参数、多轮记忆等多余功能。
