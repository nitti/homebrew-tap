# homebrew-tap

Personal Homebrew tap for tools I develop for my own use. One tap, many tools — each tool's own repo owns its release automation and pushes its formula/cask here on tag.

## Usage

```
brew tap nitti/tap
brew install nitti/tap/<tool>
```

or, without tapping first:

```
brew install nitti/tap/<tool>
```

## Tools

| Tool | Source | Description |
|------|--------|-------------|
| [dirtree](https://github.com/nitti/dirtree) | `Casks/dirtree.rb` | Terminal directory-tree browser: progressive-disclosure navigation, fuzzy-finder jump mode, syntax-highlighted preview |

## Adding a tool to this tap

A tool's own repo owns its formula/cask definition via `goreleaser` (or equivalent) and pushes updates here automatically on every tagged release — this repo is a publish target, not where formulas/casks are hand-written or maintained. To wire up a new tool:

1. In the tool's repo, add a `brews:` (formula) or `homebrew_casks:` (cask) section to its `.goreleaser.yaml` pointing at `repository: {owner: nitti, name: homebrew-tap}`.
2. Grant the tool's release workflow a `HOMEBREW_TAP_GITHUB_TOKEN` secret: a fine-grained PAT scoped to `contents: write` on this repo only.
3. Add a row to the Tools table above.
4. Tag a release in the tool's repo — the workflow pushes the formula/cask here.

Use `Casks/` for cask-style definitions (works for CLI-only binaries too, not just GUI apps) and `Formula/` for formula-style definitions, matching whichever `goreleaser` section the source repo uses.
