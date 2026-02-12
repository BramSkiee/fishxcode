# Usando FishXCode com Codex

## Instalação

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

## Configurar Variáveis de Ambiente

1. Visite [https://fishxcode.com/console/token](https://fishxcode.com/console/token) para obter sua API Key
2. Configure a variável de ambiente `FISHXCODE_TOKEN` com sua chave
3. Crie `~/.codex/config.toml`:

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

4. Crie `~/.codex/auth.json`:

```json
{
  "OPENAI_API_KEY": "sua_api_key"
}
```

## Iniciar Diretamente

```bash
cd meu-projeto
codex
```

## Usar Codex no VSCode

1. Instale a extensão Codex
2. Acesse configurações em modo JSON
3. Adicione:

```json
{
  "chatgpt.apiBase": "https://fishxcode.com/v1",
  "chatgpt.config": {
    "preferred_auth_method": "api_key",
    "model_provider": "openai-chat-completions"
  }
}
```
