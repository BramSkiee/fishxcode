# Usar FishXCode con Claude Code

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

## Configurar Variables de Entorno

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
Reemplaza `sk-xxx` con tu token de la [Consola FishXCode](https://fishxcode.com/console/token).
:::

## Lanzamiento Directo

```bash
cd mi-proyecto
claude
```

## Selección de Modelo

| Variable | Descripción |
|----------|-------------|
| `ANTHROPIC_MODEL` | Modelo principal de Claude Code |
| `ANTHROPIC_SMALL_FAST_MODEL` | Modelo rápido (obsoleto) |

### Modelos Recomendados

- `claude-sonnet-4-5-20250929`
- `claude-sonnet-4-5-20250514`
- `claude-haiku-4-5-20251001`
- `claude-3-5-haiku-20241022`

## Configuración Persistente

Agrega las variables a tu archivo de configuración del shell:

- **Linux/macOS**: `~/.bashrc` o `~/.zshrc`
- **Windows PowerShell**: `$PROFILE`
