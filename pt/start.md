# Usando FishXCode com Claude Code

## Instalar Claude Code

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

## Configurar Variáveis de Ambiente

::: code-group

```bash [Linux/macOS]
export ANTHROPIC_BASE_URL=https://fishxcode.com/
export ANTHROPIC_AUTH_TOKEN=sk-xxx
```

```powershell [Windows PowerShell]
$env:ANTHROPIC_BASE_URL="https://fishxcode.com/"
$env:ANTHROPIC_AUTH_TOKEN="sk-xxx"
```

```cmd [Windows CMD]
set ANTHROPIC_BASE_URL=https://fishxcode.com/
set ANTHROPIC_AUTH_TOKEN=sk-xxx
```

:::

::: warning Importante
Substitua `sk-xxx` pelo seu token do [Console FishXCode](https://fishxcode.com/console/token).
:::

## Iniciar Diretamente

```bash
cd meu-projeto
claude
```

## Seleção de Modelo

| Variável | Descrição |
|----------|-----------|
| `ANTHROPIC_MODEL` | Modelo principal do Claude Code |
| `ANTHROPIC_SMALL_FAST_MODEL` | Modelo rápido (obsoleto) |

### Modelos Recomendados

- `claude-sonnet-4-5-20250929`
- `claude-sonnet-4-5-20250514`
- `claude-haiku-4-5-20251001`
- `claude-3-5-haiku-20241022`

## Configuração Persistente

Adicione as variáveis ao seu arquivo de configuração do shell:

- **Linux/macOS**: `~/.bashrc` ou `~/.zshrc`
- **Windows PowerShell**: `$PROFILE`
