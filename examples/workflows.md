# Orca 典型工作流示例 | Example Workflows

个人学习整理，配合主 README 使用。命令以官方 CLI 文档为准。

## 1. 三个智能体竞速同一个功能

1. 在 Orca 里打开目标仓库，新建任务，写一条提示词（例如「给设置页加一个深色模式开关，带单元测试」）。
2. 扇出到 3 个 worktree，分别选 Claude Code、Codex、Grok。
3. 三个智能体在各自的分支并行开发；用 Quick Open 在 worktree 之间切换看进度。
4. 跑完逐份审 diff（可在 diff 行上直接标注问题回传修改），选最好的一份合并回主分支。
5. 删除落选的两个 worktree 和分支。

English: Fan one prompt out to three agents in separate worktrees, review each diff (annotate lines to send fixes back), merge the winner, delete the losers.

## 2. 手机远程盯工

1. 桌面端先把长任务派给智能体（例如全仓重构一个模块）。
2. 手机装 Orca 伴侣 App 并与桌面端配对。
3. 智能体完成或需要确认时手机收到通知；在手机上查看结果、补发后续指令。

English: Pair the mobile companion once, then monitor long-running agents and send follow-ups from your phone.

## 3. 用 Orca CLI 脚本化

```bash
# 创建一个新 worktree 并在其中启动任务（示意，参数以官方 CLI 文档为准）
orca worktree create

# 对当前界面截图，供智能体确认状态
orca snapshot
```

English: The Orca CLI (`worktree create`, `snapshot`, `click`, `fill`) lets agents and scripts drive Orca itself — useful for automated UI checks inside an agent workflow.
