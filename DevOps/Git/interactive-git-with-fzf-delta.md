# Interactive Git with fzf and Delta

Guide for inspecting git modifications interactively using fzf and delta from the terminal.

## Prerequisites

- `fzf` - Fuzzy finder
- `delta` - Git diff viewer with syntax highlighting
- `ripgrep` (optional) - For searching in diffs

## Basic Commands

### Interactive Commit Browser

Browse commits with live delta preview:

```bash
git log --oneline --color=always | fzf --ansi --preview 'git show --color=always {1} | delta' --preview-window=right:70%
```

### Interactive Commit Browser with Full View

Browse and press Enter to view full diff:

```bash
git log --oneline --color=always | fzf --ansi --preview 'git show --color=always {1} | delta' --bind 'enter:execute(git show {1} | delta | less -R)'
```

### View Specific Commit

```bash
git show <commit-hash> | delta
```

### Compare Commits

```bash
git diff <commit1>..<commit2> | delta
```

### Search Commits

Start fzf with initial search query:

```bash
git log --oneline | fzf --preview 'git show --color=always {1} | delta' --query "search-term"
```

### Browse All Branches

```bash
git log --oneline --color=always --graph --all | fzf --ansi --preview "git show --color=always {1} | delta" --preview-window=right:70%
```

## Recommended ZSH Alias

Add this to your `~/.zshrc`:

```bash
alias gfzf='git log --oneline --color=always --graph --all | fzf --ansi --preview "git show --color=always {1} | delta" --preview-window=right:70% --bind "enter:execute(git show {1} | delta | less -R)"'
```

Then reload your shell:

```bash
source ~/.zshrc
```

Usage: Just type `gfzf` in any git repository.

## Delta Configuration

Configure delta as your default git pager in `~/.gitconfig`:

```ini
[core]
    pager = delta

[interactive]
    diffFilter = delta --color-only

[delta]
    navigate = true
    side-by-side = true
    line-numbers = true
```

## Navigation Tips

- **In fzf**: Use arrow keys or `Ctrl+j`/`Ctrl+k` to navigate
- **In delta/less**: Use `n`/`N` for next/previous file, `q` to quit
- **fzf search**: Just start typing to filter commits

## Advanced Usage

### Search for Specific Code Changes

Find commits that added/removed specific code:

```bash
git log -p -S "search_term" --source --all | delta
```

### Filter by Author

```bash
git log --oneline --author="YourName" | fzf --preview 'git show --color=always {1} | delta'
```

### View Changed Files Only

```bash
git log --oneline | fzf --preview 'git show --color=always --name-only {1}'
```

### Compare Current Branch with Main

```bash
git diff main..HEAD | delta
```
