# skill233-acdesktop

> 让 Codex、DSH、Cursor、Cline、Aider 等 AI agent 通过 skill 接入 acdesktop 操控桌面。

本仓库是 [acdesktop](https://github.com/neko233-com/acdesktop) 的 skills 分拆仓——把主仓 `skills/` 目录独立出来，方便各家 AI agent 工具以 skill bundle 形式接入，而不必拉取整个 Rust 源码仓。

## 安装 acdesktop

所有 skill 都依赖 `acdesktop` CLI：

```powershell
# Windows (PowerShell)
irm https://raw.githubusercontent.com/neko233-com/acdesktop/main/scripts/install.ps1 | iex
```

```bash
# macOS arm64
curl -fsSL https://raw.githubusercontent.com/neko233-com/acdesktop/main/scripts/install.sh | bash
```

验证：

```bash
acdesktop status
```

## Skills 清单

| Skill | 触发场景 |
|-------|----------|
| `acdesktop` | 通用桌面操控——观察、行动、验证循环 |
| `acdesktop-windows` | Windows 平台差异（PowerShell 引用、UIA、Chromium/Electron） |
| `acdesktop-macos` | macOS 平台差异（TCC 权限、AX、菜单栏、通知中心） |
| `acdesktop-linux` | Linux 平台差异（AT-SPI、X11/Wayland、GTK/Qt） |
| `acdesktop-ffi` | C ABI 绑定——Python/Node/Go/Swift 直接调用 `libacdesktop_ffi` |
| `jev-desktop` | 纯语言目标驱动——不读 accessibility tree，直接给目标让模型决策 |

## 给 Codex 用

把 `skills/` 目录加入 Codex 的 skills 搜索路径，或直接复制到你的 agent workspace 的 `.codex/skills/` 下：

```bash
# 方式 1：克隆到全局
git clone https://github.com/neko233-com/skill233-acdesktop.git ~/.codex/skills/acdesktop

# 方式 2：项目级
git submodule add https://github.com/neko233-com/skill233-acdesktop.git .codex/skills/acdesktop
```

Codex 会自动识别 `SKILL.md` 的 frontmatter（name、tags、description、requirements），在对话中根据关键词触发加载。

## 给 DSH 用

```bash
# 克隆到 dsh skills 目录
git clone https://github.com/neko233-com/skill233-acdesktop.git ~/.dsh/skills/acdesktop
```

## 其他 agent

任意支持「读取 Markdown skill 文件」的 agent，把 `skills/<name>/SKILL.md` 加进它的 context 就行。

## 同步上游

本仓库与 acdesktop 主仓的 `skills/` 目录保持镜像同步。如果主仓有更新，在本仓库目录下：

```bash
git pull
```

## 仓库关系

```
neko233-com/acdesktop         主仓（Rust 源码 + skills + 二进制发布）
neko233-com/skill233-acdesktop 本仓（仅 skills/，供 AI agent 工具接入）
```

主仓每次发布新版本时会同步更新本仓的 skills 内容。
