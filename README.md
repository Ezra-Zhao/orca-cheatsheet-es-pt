# Orca 速查表 | Orca Cheatsheet | Guía rápida de Orca

> 一页看懂 Orca：把多个 AI 编程智能体（Claude Code、Codex、Grok、Cursor CLI 等）放进一个桌面工作台并行跑，各自在独立的 git worktree 里干活，你在一个地方盯进度、审 diff、合并赢家。用你自己的订阅登录，Orca 不卖模型额度。

- 上游项目：[stablyai/orca](https://github.com/stablyai/orca)（2026-10-18 实测 96,276 ★，MIT 协议，TypeScript）
- 平台：macOS / Windows / Linux 桌面端 + iOS / Android 移动伴侣
- 本页结构：中文主文 → English → Español → Português

---

## 核心概念

| 概念 | 一句话说明 |
|---|---|
| Agent（智能体） | 任何能在终端里跑的 CLI 编程助手都行：Claude Code、Codex、Grok、Cursor CLI、GitHub Copilot CLI、OpenCode、Pi、Devin CLI、Goose、Cline 等 30 多种 |
| Worktree（并行工作树） | 同一个仓库开出多个隔离的 git worktree，每个智能体在自己的工作树和分支里改代码，互不干扰 |
| Fan-out（扇出） | 把同一条提示词同时发给多个智能体并行做，最后比较结果、合并赢家 |
| Design Mode（设计模式） | 在内置 Chromium 里点任意 UI 元素，它的 HTML、CSS 和裁剪截图直接进智能体的提示词 |
| Annotate AI Diffs（标注 diff） | 在任意 diff 行上写评论，回传给智能体修改，不用离开 Orca 就能审、改、提交 |
| Mobile Companion（移动伴侣） | 手机上监控智能体进度、收到完成通知、远程补发指令 |
| Orca CLI | 智能体也能反过来驱动 Orca：用命令脚本化创建 worktree、截图、点击、填表 |
| Computer Use | 需要真实操作桌面软件时，智能体可操作可见 UI |

## 安装

官网下载（推荐）：<https://onorca.dev/download>，或从 GitHub Releases 取对应平台安装包（macOS 有 Apple Silicon 与 Intel 两个 dmg，Windows 是 exe，Linux 是 AppImage）。

```bash
# macOS（Homebrew）
brew install --cask stablyai/orca/orca

# Arch Linux（AUR，二进制包；stably-orca-git 为源码构建）
yay -S stably-orca-bin
```

移动伴侣：iOS 在 App Store 搜「Orca IDE」；Android 从官网下载 APK，与桌面端配对后使用。

## 常用操作速查

| 想做的事 | 怎么做 |
|---|---|
| 并行比较多个智能体 | 新建任务时把同一提示词扇出到多个 worktree，每个选一个智能体，跑完对比 diff 再合并 |
| 终端分屏 | 内置 Ghostty 级终端（WebGL 渲染），可无限分屏，滚动历史在重启后保留 |
| 从任务直接开工 | 内置 GitHub 与 Linear：浏览 PR、issue、项目看板，从任意任务一键开 worktree |
| 在远程机器上跑 | SSH Worktrees：智能体跑在远程大机器上，文件编辑、git、终端都在本地界面里，自动重连 + 端口转发 |
| 给智能体喂上下文 | 把文件或图片直接拖进提示词框；编辑器是 VS Code 内核，全程自动保存 |
| 全局快速打开 | Quick Open 跨 worktree、文件、智能体、命令、仓库上下文统一搜索 |
| 看额度与切账号 | 账号切换器可看 Claude 与 Codex 的用量和限流重置时间，热切换账号不用重新登录 |
| 脚本化驱动 Orca | `orca worktree create`、`snapshot`、`click`、`fill` 等 CLI 命令（见官方 CLI 文档） |
| 预览文档 | 工作区内直接预览 Markdown、图片、PDF 和仓库文档 |

## 典型工作流

1. **多方案竞速**：一个功能写一条提示词，扇出给 Claude Code、Codex、Grok 各一个 worktree，二十分钟后看三份 diff，挑最好的一份合并，其余关掉。
2. **手机盯工**：出门前在桌面端派活，路上用移动伴侣看谁先跑完、谁在等确认，直接在手机上补一句指令。
3. **设计稿改 UI**：打开内置浏览器进自己的站点，Design Mode 点中要改的元素，截图和样式自动进提示词，让智能体照着改。
4. **远程算力**：代码在本机，智能体通过 SSH worktree 跑在家里的高配机或云主机上跑构建和测试。

## 常见坑

- **Orca 不提供模型**：每个智能体都要用你自己的订阅或账号登录，额度、限流都按各家自己的规则走。
- **worktree 是真目录真分支**：合并赢家后记得删掉落选的 worktree 和分支，不然仓库里会堆一堆残留分支。
- **先审 diff 再合并**：智能体在本机以你的权限跑命令，并行扇出时一次会产生多份改动，逐份看 diff 再合并，别全盘接受。
- **移动伴侣要先配对**：手机端必须先与桌面端配对才能监控，单独装 App 没用。
- **功能更新很快**：官方自称每天发布，README 的功能列表常年滞后，真实清单看 GitHub Releases 的 changelog。

---

## English (summary)

Orca (by stablyai, MIT, ~96k stars as of 2026-10-18) is a desktop orchestrator for CLI coding agents. Run Claude Code, Codex, Grok, Cursor CLI, Copilot CLI, OpenCode, Pi and 30+ other terminal agents side by side — each in its own isolated git worktree, all tracked in one window. You bring your own subscriptions; Orca provides no model access.

Key pieces: parallel worktrees with fan-out (one prompt to many agents, compare diffs, merge the winner); Ghostty-class terminal splits whose scrollback survives restarts; Design Mode (click a UI element in the built-in Chromium and its HTML/CSS/screenshot goes straight into the prompt); native GitHub and Linear browsing; SSH worktrees on remote machines with auto-reconnect and port forwarding; diff annotation that sends line comments back to the agent; a mobile companion app (iOS/Android) for monitoring and steering; an Orca CLI (`orca worktree create`, `snapshot`, `click`, `fill`) so agents can drive Orca itself; and an account switcher with Claude/Codex usage and rate-limit tracking.

Install: download from onorca.dev, `brew install --cask stablyai/orca/orca` on macOS, `yay -S stably-orca-bin` on Arch, AppImage on Linux, setup exe on Windows.

Watch out: every agent needs your own login and quota; losing worktrees leave stray branches — clean them up after merging; review every diff before merging since agents run with your local permissions; the mobile app is useless until paired with a desktop host.

---

## Español (guía rápida — traducción de estudio, pendiente de revisión por un hablante nativo)

Orca (de stablyai, licencia MIT, ~96 mil estrellas en octubre de 2026) es un orquestador de escritorio para agentes de programación por línea de comandos. Permite ejecutar Claude Code, Codex, Grok, Cursor CLI, Copilot CLI, OpenCode, Pi y más de 30 agentes en paralelo, cada uno en su propio worktree de git aislado, con todo el seguimiento en una sola ventana. Tú aportas tus propias suscripciones: Orca no vende acceso a modelos.

Conceptos clave:

- **Worktrees en paralelo**: un mismo prompt se reparte («fan-out») entre varios agentes; al final comparas los diffs y fusionas el ganador.
- **Terminal con divisiones**: terminal de clase Ghostty con renderizado WebGL, divisiones infinitas e historial que sobrevive a los reinicios.
- **Design Mode**: haz clic en cualquier elemento de la interfaz en el navegador Chromium integrado y su HTML, CSS y captura recortada entran directamente en el prompt del agente.
- **GitHub y Linear integrados**: revisa PRs, issues y tableros sin salir de la app, y abre un worktree desde cualquier tarea.
- **Worktrees por SSH**: los agentes corren en una máquina remota potente, con reconexión automática y reenvío de puertos.
- **Anotar diffs de IA**: comenta cualquier línea del diff y envía el comentario de vuelta al agente.
- **App móvil complementaria** (iOS y Android): recibe avisos cuando un agente termina y envía instrucciones desde el teléfono.
- **Orca CLI**: los propios agentes pueden controlar Orca con comandos como `orca worktree create`, `snapshot`, `click` y `fill`.

Instalación: descarga desde onorca.dev; en macOS `brew install --cask stablyai/orca/orca`; en Arch Linux `yay -S stably-orca-bin`; en Linux general, el AppImage; en Windows, el instalador exe.

Errores frecuentes: olvidar que cada agente consume tu propia cuota; dejar ramas y worktrees perdedores sin limpiar tras fusionar; aceptar diffs sin revisarlos (los agentes actúan con tus permisos locales); instalar la app móvil sin emparejarla antes con el escritorio.

---

## Português (guia rápido — tradução de estudo, aguardando revisão de um falante nativo)

O Orca (da stablyai, licença MIT, ~96 mil estrelas em outubro de 2026) é um orquestrador de desktop para agentes de programação em linha de comando. Ele roda Claude Code, Codex, Grok, Cursor CLI, Copilot CLI, OpenCode, Pi e mais de 30 agentes em paralelo, cada um no seu próprio worktree do git, tudo acompanhado numa única janela. Você usa as suas próprias assinaturas: o Orca não fornece acesso a modelos.

Conceitos principais:

- **Worktrees em paralelo**: o mesmo prompt é distribuído («fan-out») para vários agentes; no fim você compara os diffs e faz merge do vencedor.
- **Terminal dividido**: terminal da classe do Ghostty, com renderização WebGL, divisões infinitas e histórico que sobrevive a reinicializações.
- **Design Mode**: clique em qualquer elemento da interface no Chromium embutido e o HTML, o CSS e a captura recortada vão direto para o prompt do agente.
- **GitHub e Linear nativos**: veja PRs, issues e quadros dentro do app e abra um worktree a partir de qualquer tarefa.
- **Worktrees via SSH**: os agentes rodam numa máquina remota mais forte, com reconexão automática e encaminhamento de portas.
- **Anotações em diffs de IA**: comente qualquer linha do diff e devolva o comentário ao agente.
- **Aplicativo móvel complementar** (iOS e Android): receba avisos quando um agente terminar e envie novas instruções pelo celular.
- **Orca CLI**: os próprios agentes podem dirigir o Orca com comandos como `orca worktree create`, `snapshot`, `click` e `fill`.

Instalação: baixe em onorca.dev; no macOS, `brew install --cask stablyai/orca/orca`; no Arch Linux, `yay -S stably-orca-bin`; no Linux em geral, o AppImage; no Windows, o instalador exe.

Armadilhas comuns: esquecer que cada agente consome a sua própria cota; deixar worktrees e branches perdedores acumulados depois do merge; aceitar diffs sem revisar (os agentes rodam com as suas permissões locais); instalar o app móvel sem antes pareá-lo com o desktop.

---

## 来源与声明

- 灵感来源 / Source / Fuente / Fonte: [stablyai/orca](https://github.com/stablyai/orca)
- 本仓是个人学习整理：内容用我自己的话总结自上游公开文档，不搬运原文；命令与功能以 2026-10-18 的上游 README 与官方文档为准，上游迭代很快，请以官方 changelog 为最终依据。
- 西语、葡语部分为学习译稿，待母语校对。Las secciones en español y portugués son traducciones de estudio pendientes de revisión nativa.
- License: MIT © 2026 Guangyi Zhao
