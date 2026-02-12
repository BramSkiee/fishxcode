# 在 Codex 中使用 FishXCode

## 安装 Codex

::: code-group

```bash [pnpm]
pnpm install -g @openai/codex
```

```bash [npm]
npm install -g @openai/codex
```

```bash [yarn]
yarn global add @openai/codex
```

```bash [bunx]
bunx --global @openai/codex
```

:::

## 配置环境变量

1. 访问 [https://fishxcode.com/console/token](https://fishxcode.com/console/token) 获取 API Key
2. 设置系统环境变量，变量名为 `FISHXCODE_TOKEN`，值为申请的 API Key
3. 创建 `~/.codex/config.toml` 文件，添加配置：

```toml
model = "gpt-5"
model_provider = "openai-chat-completions"
preferred_auth_method = "apikey"

[model_providers.openai-chat-completions]
name = "OpenAI using Chat Completions"
base_url = "https://fishxcode.com/v1"
env_key = "FISHXCODE_TOKEN"
wire_api = "chat"
query_params = {}
stream_idle_timeout_ms = 300000
```

4. 创建 `~/.codex/auth.json` 文件：

```json
{
  "OPENAI_API_KEY": "your_api_key_here"
}
```

## 直接启动使用

```bash
cd my-project
codex
```

## 在 VSCode 中使用

1. 安装 Codex 扩展
2. 进入设置，切换为 JSON 配置模式
3. 添加配置项：

```json
{
  "chatgpt.apiBase": "https://fishxcode.com/v1",
  "chatgpt.config": {
    "preferred_auth_method": "api_key",
    "model_provider": "openai-chat-completions"
  }
}
```

4. 点击 Codex 图标开始使用
