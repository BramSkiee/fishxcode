# 在 Claude Code 中使用 FishXCode

## 安装 Claude Code

使用以下包管理器全局安装 Claude Code CLI：

::: code-group

```bash [pnpm]
pnpm install -g @anthropic-ai/claude-code
```

```bash [npm]
npm install -g @anthropic-ai/claude-code
```

```bash [yarn]
yarn global add @anthropic-ai/claude-code
```

```bash [bunx]
bunx --global @anthropic-ai/claude-code
```

:::

## 配置环境变量

在终端设置环境变量以使用 FishXCode 的 API 服务。

::: code-group

```bash [Linux/macOS]
export ANTHROPIC_BASE_URL=https://fishxcode.com/
export ANTHROPIC_AUTH_TOKEN=sk-xxx
export ANTHROPIC_API_KEY=sk-xxx
```

```powershell [Windows PowerShell]
$env:ANTHROPIC_BASE_URL="https://fishxcode.com/"
$env:ANTHROPIC_AUTH_TOKEN="sk-xxx"
$env:ANTHROPIC_API_KEY="sk-xxx"
```

```cmd [Windows CMD]
set ANTHROPIC_BASE_URL=https://fishxcode.com/
set ANTHROPIC_AUTH_TOKEN=sk-xxx
set ANTHROPIC_API_KEY=sk-xxx
```

:::

::: warning 重要
请将 `sk-xxx` 替换为你在 [FishXCode 控制台](https://fishxcode.com/console/token) 获取的实际 Token。
:::

## 快速启动

配置完成后，进入项目目录并启动 Claude Code：

```bash
cd my-project
claude
```

## 模型选择

通过环境变量控制 Claude Code 使用的模型：

| 变量 | 说明 |
|------|------|
| `ANTHROPIC_MODEL` | Claude Code 使用的主模型 |
| `ANTHROPIC_SMALL_FAST_MODEL` | 用于轻量操作的快速模型（已弃用） |

### 推荐模型

- `claude-sonnet-4-5-20250929`
- `claude-sonnet-4-5-20250514`
- `claude-haiku-4-5-20251001`
- `claude-3-5-haiku-20241022`

### 配置示例

::: code-group

```bash [Linux/macOS]
export ANTHROPIC_MODEL=claude-sonnet-4-5-20250929
export ANTHROPIC_SMALL_FAST_MODEL=claude-3-5-haiku-20241022
claude
```

```powershell [Windows PowerShell]
$env:ANTHROPIC_MODEL = "claude-sonnet-4-5-20250929"
$env:ANTHROPIC_SMALL_FAST_MODEL = "claude-3-5-haiku-20241022"
claude
```

:::

## 持久化配置

将环境变量添加到 shell 配置文件以避免每次手动设置：

- **Linux/macOS**: 添加到 `~/.bashrc` 或 `~/.zshrc`
- **Windows PowerShell**: 添加到 `$PROFILE`
