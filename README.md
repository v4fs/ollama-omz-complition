# ollama zsh completion

Zsh tab-completion for the [`ollama`](https://ollama.com) CLI.

Completes subcommands, flags, and — dynamically — your installed model names
(via `ollama list`) and running models (via `ollama ps`).

```
$ ollama run <Tab>
gemma3:1b       ministral-3:3b
$ ollama show --<Tab>
--help        --license     --modelfile   --parameters  --system      --template    --verbose
```

## Install (oh-my-zsh)

Oh-my-zsh auto-adds `$ZSH_CUSTOM/completions/` to `$fpath` before `compinit`,
so just drop `_ollama` in there:

```sh
mkdir -p "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/completions"
cp _ollama "${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/completions/_ollama"
rm -f ~/.zcompdump*
exec zsh
```

## Install (plain zsh)

Put `_ollama` in any directory on your `$fpath`. A common choice:

```sh
mkdir -p ~/.zsh/completions
cp _ollama ~/.zsh/completions/_ollama
```

Then in `~/.zshrc`, before `compinit`:

```zsh
fpath=(~/.zsh/completions $fpath)
autoload -Uz compinit && compinit
```

Reload:

```sh
rm -f ~/.zcompdump*
exec zsh
```

## Uninstall

Delete the `_ollama` file from wherever you installed it and rebuild the cache:

```sh
rm -f ~/.zcompdump*
exec zsh
```

## Notes

- Targets ollama 0.15.x. New subcommands/flags in later versions won't complete
  until `_ollama` is updated.
- Model-name completion shells out to `ollama list` / `ollama ps`, so it
  requires a reachable Ollama server (respects `OLLAMA_HOST`).
