# Usar FishXCode con Codex

## Instalación

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

## Configurar Variables de Entorno

1. Visita [https://fishxcode.com/console/token](https://fishxcode.com/console/token) para obtener tu API Key
2. Configura la variable de entorno `FISHXCODE_TOKEN` con tu clave
3. Crea `~/.codex/config.toml`:

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

4. Crea `~/.codex/auth.json`:

```json
{
  "OPENAI_API_KEY": "tu_api_key"
}
```

## Lanzamiento Directo

```bash
cd mi-proyecto
codex
```

## Usar Codex en VSCode

1. Instala la extensión Codex
2. Accede a configuración en modo JSON
3. Agrega:

```json
{
  "chatgpt.apiBase": "https://fishxcode.com/v1",
  "chatgpt.config": {
    "preferred_auth_method": "api_key",
    "model_provider": "openai-chat-completions"
  }
}
```
