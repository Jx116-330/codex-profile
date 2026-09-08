# Codex Profile

一套可跨电脑迁移的个人 Codex 配置，记录我的工作习惯、嵌入式开发协作方式和常用工作流，供自己同步，也供其他 Codex 用户参考。

## 包含内容

- `AGENTS.md`：全局工作准则，包括沟通方式、变更边界、验证要求和安全约束。
- `skills/engineer-partner/`：面向 TC387 多核固件、嵌入式开发和实车调参的个人 skill。
- `config.toml.example`：可迁移的 Codex 配置示例，不包含凭据和机器专用路径。
- `NEW-PC-SETUP-PROMPT.md`：在新电脑上让 Codex 自动完成迁移的提示词。

## 在新电脑上迁移

先安装 Codex，并使用自己的账号完成登录，然后执行：

1. 将 `AGENTS.md` 复制到 `$CODEX_HOME/AGENTS.md`。未设置 `CODEX_HOME` 时，通常是 `~/.codex/AGENTS.md`。
2. 将 `skills/` 下的内容合并到全局 skills 目录，通常是 `~/.agents/skills/`。
3. 阅读 `config.toml.example`，只把适用于当前电脑的设置合并到本机 `config.toml`。
4. 在新电脑上重新配置 MCP servers、plugins、hooks、provider 和凭据。
5. 重启 Codex，并让它列出当前加载的 `AGENTS.md` 和可用 skills。

也可以直接复制 [NEW-PC-SETUP-PROMPT.md](NEW-PC-SETUP-PROMPT.md) 中的提示词，让新电脑上的 Codex 执行迁移。

## 在项目中使用

如果规则只适用于某个项目，建议把项目专属的 `AGENTS.md` 放在项目根目录，而不是加入全局配置。Codex 会将全局规则与项目目录下的规则按目录层级合并，越靠近当前工作目录的规则优先级越高。

## 安全边界

本仓库只保存可公开分享的说明和配置模板，刻意不包含：

- `auth.json`、API keys、tokens 或其他凭据；
- session、SQLite 数据库、历史记录、日志和缓存；
- 依赖某台电脑盘符、用户名或安装位置的绝对路径。

如果你基于本仓库扩展配置，请先检查 Git 历史和待提交文件，确认没有敏感信息。

## 免责声明

这里的规则体现个人工作偏好，不是 Codex 官方默认配置。使用前请根据自己的项目、操作系统和安全要求进行审查和调整。
