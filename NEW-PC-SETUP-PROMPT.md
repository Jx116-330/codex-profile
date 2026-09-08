# New Computer Setup Prompt

Copy the following prompt into Codex on the new computer after cloning this repository.

```text
你是 Codex 配置迁移助手。当前目录是我的 codex-profile 仓库。请先阅读 README.md、AGENTS.md 和 config.toml.example，然后把这套个人配置安装到当前电脑。

要求：
1. 检测当前操作系统、CODEX_HOME；没有设置时使用该系统默认 Codex home。
2. 先检查目标位置已有的 AGENTS.md、config.toml 和 skills，并在覆盖前创建带时间戳的备份。
3. 将本仓库的 AGENTS.md 安装为全局 AGENTS.md。
4. 将 skills/ 下的个人 skills 合并到全局 skills 目录；不要删除目标电脑已有的其他 skills。
5. 参考 config.toml.example，把便携设置合并到本机 config.toml；不要覆盖已有的认证、MCP、插件、hooks、provider、路径或机器相关配置。
6. 不要复制或创建 auth.json、token、API key、session、sqlite、日志、缓存，也不要把任何凭据提交到 GitHub。
7. 检查 AGENTS.md 和 skill 文件中是否还有当前电脑不存在的绝对路径；能根据当前工作区改成相对定位就改，否则列出待人工处理项。
8. 完成后报告：实际写入的文件、备份位置、未自动迁移的配置，以及需要重启 Codex 才能生效的项目。
9. 最后验证当前 Codex 能发现全局 AGENTS.md 和 engineer-partner skill。不要执行 git push，也不要修改这个 GitHub 仓库。
```
