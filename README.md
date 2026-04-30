<div align="center">

# 📝 Weekly Report Skill

**让 AI 替你写周报 —— 从飞书学习日报一键生成结构化工作周报**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-8A2BE2?logo=anthropic&logoColor=white)](https://docs.anthropic.com/en/docs/claude-code)
[![Lark](https://img.shields.io/badge/Feishu-Lark%20CLI-00D6B9?logo=lark&logoColor=white)](https://github.com/larksuite/cli)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/Friday-Up/weekly-report/pulls)
[![GitHub Stars](https://img.shields.io/github/stars/Friday-Up/weekly-report?style=social)](https://github.com/Friday-Up/weekly-report)

[功能特性](#-功能特性) • [快速开始](#-快速开始) • [使用方法](#-使用方法) • [周报结构](#-周报结构) • [常见问题](#-常见问题) • [贡献](#-贡献)

</div>

---

## 📖 简介

**Weekly Report Skill** 是一个为 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) 打造的 Skill，它能够：

- 自动从**飞书汇报（学习日报）**拉取你一周的工作记录；
- 通过 LLM 智能**归类、合并、提炼**碎片化的每日进展；
- 按照固定模板和写作风格，**一键生成**可直接发送的结构化周报。

> 把"每周憋周报"的两小时还给你 ⏱️

---

## ✨ 功能特性

| 特性 | 说明 |
| --- | --- |
| 🤖 **全自动拉取** | 通过 `lark-cli` 调用飞书汇报 API，自动获取指定周的日报数据 |
| 🧠 **智能归类合并** | 同一项目不同天的进展自动合并到一条工作线，去除冗余 |
| 🎯 **状态智能识别** | 自动识别 ✅ 已完成 / 🔵 进行中 / ❌ 未开始 / ⏸ 已暂停 |
| 📐 **固定模板输出** | 严格遵循「核心任务 → 学习与思考 → 下周计划」三段式结构 |
| 📅 **下周计划推断** | 基于未完成项 + 进行中项，按高/中/低优先级智能生成 |
| ⚙️ **个性化配置** | 签名、抬头、文件名前缀均可通过 `config.json` 自定义 |
| 🗣️ **自然语言触发** | 一句"帮我写本周周报"即可，无需记忆任何命令 |

---

## 🚀 快速开始

### 前置依赖

| 依赖 | 说明 |
| --- | --- |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Anthropic 官方 CLI，需先完成安装与登录 |
| [lark-cli](https://github.com/larksuite/cli) | 飞书命令行工具，需完成 `lark-cli auth login` 授权 |
| 飞书学习日报 | 你的飞书汇报中需存在「学习日报」类型的日报数据 |

### 安装

#### 方式一：通过 `npx skills` 一键安装（推荐）

```bash
npx skills add Friday-Up/weekly-report -y -g
```

#### 方式二：手动克隆 + 软链接

```bash
# 1. 克隆仓库
git clone https://github.com/Friday-Up/weekly-report.git
cd weekly-report

# 2. 软链接到 Claude Code skills 目录
ln -s "$(pwd)" ~/.claude/skills/weekly-report

# 3. 复制示例配置
cp config.example.json config.json
```

### 配置

编辑 `config.json`，填入你的个人信息：

```json
{
  "user_open_id": "ou_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "author_name": "张三",
  "author_title": "高级工程师",
  "company": "XX 科技有限公司",
  "mobile": "138-0000-0000",
  "email": "zhangsan@example.com",
  "address": "北京市朝阳区 XX 大厦",
  "file_prefix": "技术部-张三-工作周报"
}
```

> 💡 **如何获取 `user_open_id`？**
>
> ```bash
> lark-cli auth status
> ```
> 输出中的 `userOpenId` 字段即为所需值。

---

## 💬 使用方法

在 Claude Code 中用自然语言对话即可触发：

```text
帮我写本周周报
```

```text
帮我写 4.20-4.24 的周报
```

```text
生成上周周报
```

```text
总结下本周工作
```

生成的周报将以 Markdown 格式保存在 `docs/` 目录下，文件名形如：

```text
docs/技术部-张三-工作周报（4.20-4.24）.md
```

---

## 📑 周报结构

生成的周报严格遵循以下三段式结构：

```text
各位领导、管培生小伙伴们：

大家好！本周（M.DD-M.DD）主要围绕 {核心工作线} 展开 ……

一、核心任务
  1. {工作线 1}
     - 进展：……
     - 待推进事项：……
     - 成果：……
  2. {工作线 2}
     ……

二、学习与思考
  1. {主题}：{结合本周工作的方法论提炼}
  2. ……
  3. ……

三、下周工作计划
  1. 【高优先级】……
  2. 【中优先级】……
  3. 【低优先级】……

————————————
{签名信息}
```

详细的写作风格规范请参见 [`SKILL.md`](./SKILL.md)。

---

## 🗂️ 目录结构

```text
weekly-report/
├── SKILL.md              # Skill 定义与提示词（核心逻辑）
├── README.md             # 项目说明（你正在看的文件）
├── LICENSE               # MIT 协议
├── config.example.json   # 配置模板
├── config.json           # 个人配置（已 .gitignore，不会提交）
├── docs/                 # 生成的周报输出目录（已 .gitignore）
│   └── .gitkeep
└── .gitignore
```

---

## ❓ 常见问题

<details>
<summary><b>Q1：执行后提示 <code>lark-cli: command not found</code></b></summary>

请先安装并登录 [lark-cli](https://github.com/larksuite/cli)：

```bash
npm install -g @larksuiteoapi/lark-cli
lark-cli auth login
```
</details>

<details>
<summary><b>Q2：拉取的数据为空 / 不是「学习日报」</b></summary>

确认你的飞书汇报中存在「学习日报」类型，并且 `user_open_id` 填写正确。可通过 `lark-cli auth status` 重新核对。
</details>

<details>
<summary><b>Q3：生成的周报风格不符合我的期望</b></summary>

直接编辑 [`SKILL.md`](./SKILL.md) 中的「写作风格要求」章节，定制你自己的语言风格、模板结构和优先级判定规则。
</details>

<details>
<summary><b>Q4：能否支持其他来源（钉钉 / 企微 / 自定义）？</b></summary>

当前版本仅支持飞书学习日报。如有需求欢迎提 [Issue](https://github.com/Friday-Up/weekly-report/issues) 或 PR。
</details>

---

## 🤝 贡献

欢迎任何形式的贡献！

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/amazing-feature`
3. 提交变更：`git commit -m 'feat: add amazing feature'`
4. 推送分支：`git push origin feature/amazing-feature`
5. 提交 Pull Request

提交信息请遵循 [Conventional Commits](https://www.conventionalcommits.org/) 规范。

---

## 📜 License

本项目基于 [MIT License](./LICENSE) 开源协议发布。

---

## 🌟 致谢

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) —— 强大的 AI 编程助手
- [lark-cli](https://github.com/larksuite/cli) —— 飞书官方命令行工具
- 所有为本项目提供反馈和建议的小伙伴 ❤️

<div align="center">

**如果这个 Skill 帮到了你，欢迎点一个 ⭐ Star 支持一下！**

</div>