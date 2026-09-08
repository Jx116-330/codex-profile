# Codex Profile

Portable personal Codex guidance for use across computers.

## Install on a new computer

1. Install Codex and sign in normally.
2. Copy `AGENTS.md` to `$CODEX_HOME/AGENTS.md` (usually `~/.codex/AGENTS.md`).
3. Copy the contents of `skills/` to `~/.agents/skills/`.
4. Review `config.toml.example` and apply only portable settings to the local `config.toml`.
5. Reconfigure MCP servers, plugins, hooks, and credentials for the new machine.
6. Restart Codex and ask it to list the active instruction files.

Never copy authentication files, session databases, logs, caches, or machine-specific absolute paths.
