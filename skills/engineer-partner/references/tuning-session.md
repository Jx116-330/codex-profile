# Tuning Session — 调车/调参会话协议

实车调车、PID/参数调整、遥测判读、轨迹图分析的领域细则。本文件在调车任务时读取。

## 契约（单一权威源）

本 Skill 只存元规则，不复制手册内容。调车会话期间：

- **开场**：先在当前工作区定位并读取 `TUNING_PLAYBOOK.md`（唯一权威操作手册）。读完即续任务，不去源码考古命令格式
- **结束**：用户说"结束调车"时，必须立刻更新手册 §9 会话日志、§7 经验库、§8 当前状态快照
- **瘦身纪律**：手册只装"当前活的"（~300 行）；被取代的经验/旧快照/往期日志逐字搬去同一工具目录下的 `TUNING_HISTORY.md`（只增不删）；§9 只留最近 1~3 场
- 手册仅在调车操作流程和参数口径上优先于本 Skill；本 Skill 与全局危险动作确认要求仍适用
- 下次调车作战计划：同一工具目录下的 `NEXT_SESSION.md`（会过期，以最新一次更新为准）

## 发车铁律

- 发车前**必问**用户，等明确"发车"指令；绝不脚本一键发车
- 上一轮授权 ≠ 这一轮授权；每次发车独立确认
- 车摆到起点后发车

## 调参纪律

- 调参参数一律走 TCP 入口（setter/getter + dispatch + 遥测回显 + 文档四件套）；`#define` 只做上电默认
- 极性类参数范围必须允许负值
- 改参数后看遥测回显确认生效，不背记忆数字
- 已定案参数：若用户在当前任务中明确说明参数状态、名称和目标值，则视为该次变更已确认；状态或范围不明确时，在写入前确认（临时试验值 vs 定案值）

## 数据验证

- 每趟跑完必看轨迹图（cpx/cpy vs 录制线 PNG），不只报统计数字；偏差说空间位置
- 物理偏现场量（遥测对 DR 绝对漂/侧滑全盲）；遥测 xte 干净 ≠ 物理不偏
- 数据恢复：工具项目中的 `dist/runtime/telemetry_history.jsonl`
- 开场标配 `python archive.py watch` 自动切趟归档；list/compare/session-summary

## 链路开场

- PC 工具位于当前项目的调车工具目录（根目录 13 个活 py）；YawTuningTool.exe = TCP↔HTTP 桥（自动 HB 保活）
- dashboard.html 热加载改 cp 即生效；config.json 改后重启 exe；改 tuning_tool.py 必重打 exe
- 高频轮询会堵桥导致假 abort（遥测 ~12Hz 天花板）；数据从 telemetry_history.jsonl 恢复
- 保活/发车一切走 session_driver.py

## 固件/状态约定

- 比赛固件 HEAD：以 TUNING_PLAYBOOK §8 为准，不背记忆
- 烧旧固件时 Gate8 → TCP 发车假 abort（lostsrc=32），只用菜单发车
- 鉴别真重启：tcpok→0 + reconn++，不看 42.95s 回绕时钟
