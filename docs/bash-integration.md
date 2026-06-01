## Bash integration

Bash script to help with prompting

Open:

```sh
code ~/.bashrc
```

Paste this at the bottom:

```sh
prompt () {
  local action="$1"
  local project="$2"

  if [ -z "$action" ] || [ -z "$project" ]; then
    echo "Usage: prompt <requirements|requirements-reverse|feature|feature-reverse|implementation|code-files|documentation|commit-message|explanation|translation-en-pl> <project>"
    return 1
  fi

  local root="$HOME/atari-monk/project"
  local pyUtils="$root/scripts/scripts/python"
  local prompts="$root/prompts/prompts"
  local promptScript="$pyUtils/prompt-assembler.py"
  local map="$root/$project/.config/prompt-map.json"

  case "$action" in
    requirements)
      python3 "$promptScript" "$prompts/requirements.md" "$map"
      ;;
    requirements-reverse)
      python3 "$promptScript" "$prompts/requirements-reverse.md" "$map"
      ;;
    feature)
      python3 "$promptScript" "$prompts/feature.md" "$map"
      ;;
    feature-reverse)
      python3 "$promptScript" "$prompts/feature-reverse.md" "$map"
      ;;
    implementation)
      python3 "$promptScript" "$prompts/implementation.md" "$map"
      ;;
    code-files)
      python3 "$promptScript" "$prompts/code-files.md" "$map"
      ;;
    documentation)
      python3 "$promptScript" "$prompts/documentation.md" "$map"
      ;;
    commit-message)
      python3 "$promptScript" "$prompts/commit-message.md" "$map"
      ;;
    explanation)
      python3 "$promptScript" "$prompts/explanation.md" "$map"
      ;;
    translation-en-pl)
      python3 "$promptScript" "$prompts/translation-en-pl.md" "$map"
      ;;
    *)
      echo "Unknown action: $action"
      echo "Use: commit | docs"
      return 1
      ;;
  esac
}
```

Reload bash

```sh
source ~/.bashrc
```

Use it

Type for help:

```sh
prompt
```

Example

```sh
prompt requirements scripts
```