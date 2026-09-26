# ContextRelay

AI Relay：把 **Codex（规划）** 与 **豆包（执行）** 桥接起来的 Windows 本地桌面协调工具。

- **Codex**：理解目标，产出执行策略，通过 MCP 工具下发任务、验收结果。
- **豆包**：在「工作模式」下真实执行（读写文件、排版、生成 Word/PDF 等）。
- **AI Relay**：编排、RPA（CDP 自动驱动豆包 UI）、状态机与 SQLite 存储。

## 一键安装（推荐，装完即用）

1. **前置**：先装好并登录 **豆包桌面客户端** 和 **Codex 桌面应用**（这两个是外部依赖，安装包不包含）。
2. 到 [Releases](https://github.com/xingyaunbo/ContextRelay/releases) 下载最新 `ContextRelay-Setup.exe`，双击安装。
3. 安装完成后**自动**做好两件收尾（`postinstall.ps1`）：
   - 把 ai-relay 技能安装到 `~/.agents/skills/ai-relay/SKILL.md`
   - 把 `ContextRelay-MCP.exe` 注册进 `~/.codex/config.toml` 的 `[mcp_servers.aiRelay]`
4. **完全退出 Codex 再重新打开**（让 MCP server + skill 重新加载）。
5. 在 Codex 里直接说，例如：

   > 帮我做一份《唐诗三十首》的 Word 文档，每首含题目、作者和全文，交给豆包执行。

   Codex 会走：ai-relay skill → `relay_execute_task`（异步提交）→ 豆包工作模式执行 → `relay_get_result` 轮询 → 拿到结果回复你。

> 安装包默认装到 `C:\Users\<你的用户名>\AppData\Local\Programs\ContextRelay\`（免管理员）。

## 源码部署（开发者）

从零用源码跑（改代码、二次开发）见 [DEPLOY.md](DEPLOY.md)。

## 目录结构

| 目录/文件 | 说明 |
| --- | --- |
| `agents/` | Codex 客户端与规划提示词 |
| `core/` | 编排、任务契约、文件任务 |
| `rpa/` | 豆包 CDP 自动化、窗口操作 |
| `storage/` | SQLite 存储 |
| `ui/` | GUI（主界面 + 悬浮侧边窗） |
| `mcp_server.py` | MCP server（Codex 调用入口） |
| `skills/ai-relay/SKILL.md` | Codex 的 ai-relay skill |
| `config.py` | 全局配置 |
| `postinstall.ps1` | 安装后自动装 skill + 注册 MCP |
| `installer.iss` | Inno Setup 安装包脚本 |

## 文档

- [使用手册.md](使用手册.md) —— 完整功能说明
- [DEPLOY.md](DEPLOY.md) —— 从零部署教程

## 许可

本仓库提供源码与使用说明，供学习与自用。
