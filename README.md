# ContextRelay

AI Relay：把 **Codex（规划）** 与 **豆包（执行）** 桥接起来的 Windows 本地桌面协调工具。

- **Codex**：理解目标，产出执行策略，通过 MCP 工具下发任务、验收结果。
- **豆包**：在「工作模式」下真实执行（读写文件、排版、生成 Word/PDF 等）。
- **AI Relay**：编排、RPA（CDP 自动驱动豆包 UI）、状态机与 SQLite 存储。

## 一键安装（装完即用）

1. **前置**：先装好并登录 **豆包桌面客户端** 和 **Codex 桌面应用**（这两个是外部依赖，安装包不包含）。
2. 到 [Releases](https://github.com/xingyaunbo/ContextRelay/releases) 下载最新 `ContextRelay-Setup.exe`（当前 v1.1.2），双击安装。
3. 安装完成后**自动**做好两件收尾（`postinstall.ps1`）：
   - 把 ai-relay 技能安装到 `~/.agents/skills/ai-relay/SKILL.md`
   - 把 `ContextRelay-MCP.exe` 注册进 `~/.codex/config.toml` 的 `[mcp_servers.aiRelay]`
4. **完全退出 Codex 再重新打开**（让 MCP server + skill 重新加载）。
5. 在 Codex 里直接说，例如：

   > 帮我做一份《唐诗三十首》的 Word 文档，每首含题目、作者和全文，交给豆包执行。

   Codex 会走：ai-relay skill → `relay_execute_task`（异步提交）→ 豆包工作模式执行 → `relay_get_result` 轮询 → 拿到结果回复你。

> 安装包默认装到 `C:\Users\<你的用户名>\AppData\Local\Programs\ContextRelay\`（免管理员）。
> 豆包客户端安装位置无需特殊配置，Relay 会自动探测并自动驱动。

## 侧边窗（可选的可视化面板）

安装后桌面/开始菜单里的 **ContextRelay** 是侧边窗，用于查看会话、切换豆包电脑。它常驻系统托盘：

- 点窗口的 **×** 不会退出，而是最小化到右下角系统托盘，后台继续运行。
- 托盘图标右键 →「退出」才真正结束进程；单击/双击托盘图标可重新打开窗口。

## 最近更新

- **v1.1.2**：侧边窗点 × 最小化到系统托盘（右键退出），解决「窗口关了进程还在、托盘找不到」的问题。
- **v1.1.1**：自动探测豆包安装路径，修复换机器后豆包被强杀却重启失败导致的闪退。
- **v1.1.0**：一键安装（自动装 ai-relay skill + 注册 aiRelay MCP server），装完即用。

## 源码

本仓库仅公开 README 与 Release 安装包，源码不公开。
