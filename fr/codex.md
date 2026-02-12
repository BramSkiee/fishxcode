# Utiliser FishXCode avec Codex

## Installation

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

## Configuration des Variables d'Environnement

1. Obtenez votre clé API sur [https://fishxcode.com/console/token](https://fishxcode.com/console/token)
2. Définissez une variable d'environnement `FISHXCODE_TOKEN` avec votre clé
3. Créez `~/.codex/config.toml` :

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

4. Créez `~/.codex/auth.json` :

```json
{
  "OPENAI_API_KEY": "votre_clé_api"
}
```

## Démarrage Direct

```bash
cd mon-projet
codex
```

## Utiliser Codex dans VSCode

1. Installez l'extension Codex
2. Accédez aux paramètres et passez en mode JSON
3. Ajoutez :

```json
{
  "chatgpt.apiBase": "https://fishxcode.com/v1",
  "chatgpt.config": {
    "preferred_auth_method": "api_key",
    "model_provider": "openai-chat-completions"
  }
}
```

4. Cliquez sur l'icône Codex pour commencer
