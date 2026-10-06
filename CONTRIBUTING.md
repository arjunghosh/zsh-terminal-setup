# Contributing

Thanks for helping. Keep changes small and focused.

1. Open an issue first for anything bigger than a typo, so we can agree on the approach.
2. Shell scripts must pass `shellcheck`; Zsh files must pass `zsh -n <file>`.
3. Scripts must stay compatible with **Bash 3.2** (the macOS default) and must never delete user files — move them to a backup instead.
4. Pin any new upstream dependency to a tag or commit.
5. Update `CHANGELOG.md` under `[Unreleased]` in the same pull request.
6. Never commit secrets, tokens, or personal paths. Machine-specific settings belong in `~/.zshrc.local`.

By contributing you agree your work is licensed under the [MIT License](LICENSE).
