# Utiliser FishXCode avec Claude Code

## Installation de Claude Code

Installez Claude Code globalement en utilisant votre gestionnaire de paquets préféré :

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

## Configuration des Variables d'Environnement

Configurez votre système pour utiliser l'API FishXCode :

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

::: warning Important
Remplacez `sk-xxx` par votre clé API obtenue sur la [Console FishXCode](https://fishxcode.com/console/token).
:::

## Lancement Direct

Après configuration, accédez au répertoire de votre projet et démarrez Claude Code :

```bash
cd mon-projet
claude
```

## Sélection du Modèle

Contrôlez les modèles via variables d'environnement :

| Variable | Description |
|----------|-------------|
| `ANTHROPIC_MODEL` | Modèle principal utilisé par Claude Code |
| `ANTHROPIC_SMALL_FAST_MODEL` | Modèle rapide pour opérations légères (obsolète) |

### Modèles Recommandés

- `claude-sonnet-4-5-20250929`
- `claude-sonnet-4-5-20250514`
- `claude-haiku-4-5-20251001`
- `claude-3-5-haiku-20241022`

## Configuration Persistante

Ajoutez les variables d'environnement à votre fichier de configuration shell :

- **Linux/macOS** : `~/.bashrc` ou `~/.zshrc`
- **Windows PowerShell** : `$PROFILE`
