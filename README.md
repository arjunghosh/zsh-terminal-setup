# zsh-terminal-setup

**An opinionated, Monokai-styled Zsh terminal for macOS — and a makeover you can undo.**

Oh My Zsh + Powerlevel10k + autosuggestions + syntax highlighting + MesloLGS NF, tuned to look
consistent with Sublime Text's Monokai palette.

> **Status: pre-release (working towards v0.1.0).** The configuration files work today and can be
> installed by hand (below). The automated `install.sh` / `uninstall.sh` with backups and one-command
> rollback is in progress — see [Roadmap](#roadmap).

---

## What you get

| Component | Role |
|---|---|
| [Zsh](https://www.zsh.org/) | Shell |
| [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) | Plugin and theme framework |
| [Powerlevel10k](https://github.com/romkatv/powerlevel10k) | Fast, status-aware prompt (config in `.p10k.zsh`) |
| [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) | Suggests commands from history as you type |
| [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) | Colours commands while you type; invalid ones turn red |
| MesloLGS NF font | Nerd Font with the icons the prompt needs |
| Monokai-inspired colours | Consistent look across prompt and terminal |

## Requirements

- macOS (tested on Sonoma 14.x, Apple Silicon). Linux/WSL: untested.
- `zsh`, `git`, `curl` (all preinstalled on recent macOS).
- A terminal that supports true colour and custom fonts (iTerm2 recommended).

## Manual install (current)

> **Back up first.** These steps overwrite `~/.zshrc` and `~/.p10k.zsh`.

```bash
# 1. Back up your current config
mkdir -p ~/.zsh-setup-backup/manual
cp ~/.zshrc ~/.p10k.zsh ~/.zsh-setup-backup/manual/ 2>/dev/null

# 2. Install Oh My Zsh WITHOUT letting it start a new shell or replace your .zshrc.
#    Read the script first: https://github.com/ohmyzsh/ohmyzsh/blob/master/tools/install.sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended --keep-zshrc

# 3. Theme + plugins (pinned to tested versions)
ZSH_CUSTOM="${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}"
git clone --depth=1 --branch v1.20.0 https://github.com/romkatv/powerlevel10k.git "$ZSH_CUSTOM/themes/powerlevel10k"
git clone --depth=1 --branch v0.7.1 https://github.com/zsh-users/zsh-autosuggestions "$ZSH_CUSTOM/plugins/zsh-autosuggestions"
git clone --depth=1 --branch 0.8.0 https://github.com/zsh-users/zsh-syntax-highlighting.git "$ZSH_CUSTOM/plugins/zsh-syntax-highlighting"

# 4. Copy the configs from this repo
cp .zshrc .p10k.zsh ~/
```

5. **Font:** download the four MesloLGS NF files from the
   [Powerlevel10k font instructions](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k),
   double-click each to install, then set your terminal font to **MesloLGS NF**.
6. Open a new terminal tab.

### Known issue (fixed in v0.1.0)

`.zshrc` currently also sources Powerlevel10k from `/opt/homebrew/share/powerlevel10k/`, a path that only
exists on Apple Silicon Macs with the Homebrew package. If you see
`no such file or directory: /opt/homebrew/...`, delete that `source` line — the theme is already loaded
through `ZSH_THEME`.

## Undo (manual)

```bash
cp ~/.zsh-setup-backup/manual/.zshrc ~/.zsh-setup-backup/manual/.p10k.zsh ~/ 2>/dev/null
```

Then open a new tab. Oh My Zsh, plugins and fonts stay installed; remove them separately if you wish.

## Troubleshooting

| Symptom | Cause / fix |
|---|---|
| Boxes or `?` instead of icons | Terminal font is not set to **MesloLGS NF** |
| Prompt wizard starts every time | `~/.p10k.zsh` is missing — copy it from this repo, or run `p10k configure` |
| `plugin 'zsh-autosuggestions' not found` | Step 3 did not complete — re-run the `git clone` lines |
| Slow startup | Measure with `time zsh -i -c exit`; disable plugins one by one |

## Roadmap

**v0.1.0 — safe installer**
- `install.sh`: backs up every file it replaces into `~/.zsh-setup-backup/<timestamp>/`, safe to re-run,
  `--dry-run`, OS/architecture detection, pinned upstream versions, `~/.zshrc.local` override hook.
- `uninstall.sh`: restores your previous files from the newest backup.
- Font installer that downloads MesloLGS NF and verifies SHA-256 checksums.
- Repo layout: `dotfiles/`, `themes/`, `fonts/`, `tests/`.
- Tests: `shellcheck`, `zsh -n`, bats behaviour tests (including install → uninstall restores files
  byte-for-byte), and GitHub Actions on macOS + Ubuntu.

**Later:** iTerm2 profile import, startup-time budget in CI, optional Starship prompt (Powerlevel10k
upstream now has [very limited support](https://github.com/romkatv/powerlevel10k)).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Security issues: see [SECURITY.md](SECURITY.md).

## License

[MIT](LICENSE) © 2025–2026 Arjun Ghosh. Third-party components keep their own licenses (below).

## Credits

| Project | License |
|---|---|
| [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) | MIT |
| [Powerlevel10k](https://github.com/romkatv/powerlevel10k) by Roman Perepelitsa | MIT |
| [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) | MIT |
| [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) | BSD-3-Clause |
| MesloLGS NF (Meslo, derived from Apple Menlo / Bitstream Vera; glyphs from Nerd Fonts) | Apache License 2.0 |
| Colour palette inspired by Monokai (Sublime Text) | — (inspiration only; no files copied) |

---

Author: **Arjun Ghosh** · [LinkedIn](https://www.linkedin.com/in/arjunghosh)
