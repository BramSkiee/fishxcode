# Using FishXCode with Claude Code

## Install Claude Code

Install the Claude Code CLI globally using your preferred package manager:

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

## Configure Environment Variables

Set up your terminal environment variables to connect with FishXCode's API service.

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

::: warning Important
Replace `sk-xxx` with your actual token from the [FishXCode Console](https://fishxcode.com/console/token).
:::

## Launch Directly

After configuring variables, navigate to your project and launch Claude Code:

```bash
cd my-project
claude
```

## Model Selection

Control which Claude model Claude Code uses through environment variables:

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_MODEL` | Primary model for Claude Code |
| `ANTHROPIC_SMALL_FAST_MODEL` | Fast model for lightweight operations (deprecated) |

### Recommended Models

- `claude-sonnet-4-5-20250929`
- `claude-sonnet-4-5-20250514`
- `claude-haiku-4-5-20251001`
- `claude-3-5-haiku-20241022`

### Configuration Example

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

## Persistent Configuration

Add environment variables to your shell configuration file to avoid manual setup each session:

- **Linux/macOS**: Add to `~/.bashrc` or `~/.zshrc`
- **Windows PowerShell**: Add to `$PROFILE`
