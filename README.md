# ollama zsh completion

Zsh tab-completion for the [`ollama`](https://ollama.com) CLI.

Completes subcommands, flags, and — dynamically — your installed models
(`ollama list`) and running models (`ollama ps`).

```
$ ollama run <Tab>
gemma3:1b       ministral-3:3b
$ ollama show --<Tab>
--help        --license     --modelfile   --parameters  --system      --template    --verbose
```

## Install

**oh-my-zsh:**

```sh
mkdir -p "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/completions"
cp _ollama "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/completions/_ollama"
omz reload
```

**plain zsh:** copy `_ollama` into any directory on your `$fpath`, e.g.:

```sh
mkdir -p ~/.zsh/completions
cp _ollama ~/.zsh/completions/_ollama
```

Then add this to `~/.zshrc` (before `compinit`):

```zsh
fpath=(~/.zsh/completions $fpath)
autoload -Uz compinit && compinit
```

Reload:

```sh
exec zsh
```

## Uninstall

```sh
rm /path/to/_ollama && exec zsh
```

## Notes

- The whole thing was one shoted with Claude
- Targets ollama 0.15.x. Newer subcommands/flags won't complete until `_ollama` is updated.
- Model-name completion calls `ollama list` / `ollama ps`, so a reachable Ollama server is required (respects `OLLAMA_HOST`).
- If completion doesn't appear after reload, clear zsh's cache: `rm -f ~/.zcompdump* && exec zsh`.
