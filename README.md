# Weekly Report Skill

一个 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skill，从飞书学习日报自动生成结构化工作周报。

## 功能

- 自动获取飞书汇报（学习日报）中指定周的每日工作记录
- 智能归类合并同一项目不同天的碎片化进展
- 按固定模板和写作风格生成结构化周报
- 从未完成项和进行中事项智能推断下周工作计划

## 前置条件

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [lark-cli](https://github.com/larksuite/cli)（已安装并完成登录授权）
- 飞书汇报中有"学习日报"类型的日报数据

## 安装

### 方式一：手动安装

```bash
# 克隆仓库
git clone https://github.com/Friday-Up/weekly-report.git

# 创建软链接到 Claude Code skills 目录
ln -s $(pwd)/weekly-report ~/.claude/skills/weekly-report

# 复制示例配置并填写个人信息
cp weekly-report/config.example.json weekly-report/config.json
```

### 方式二：通过 npx skills 安装

```bash
npx skills add Friday-Up/weekly-report -y -g
```

## 配置

复制 `config.example.json` 为 `config.json`，填写个人信息：

```json
{
  "user_open_id": "your_open_id_here",
  "author_name": "你的名字",
  "author_title": "你的职位",
  "company": "你的公司",
  "mobile": "你的手机号",
  "email": "你的邮箱",
  "address": "你的地址",
  "file_prefix": "部门-姓名-工作周报"
}
```

获取 `user_open_id`：

```bash
lark-cli auth status
# 输出中的 userOpenId 即为所需值
```

## 使用

在 Claude Code 中直接对话即可：

```
帮我写本周周报
```

```
帮我写 4.20-4.24 的周报
```

```
生成上周周报
```

生成的周报将保存在 `docs/` 目录下。

## 周报结构

生成的周报包含以下部分：

1. **核心任务** — 按工作线组织，包含进展、待推进事项和成果
2. **学习与思考** — 结合本周工作提炼的 3 条方法论思考
3. **下周工作计划** — 按高/中/低优先级智能推断

## 目录结构

```
weekly-report/
├── SKILL.md              # Skill 定义
├── config.example.json   # 配置示例
├── config.json           # 个人配置（不提交）
├── .gitignore
├── docs/                 # 生成的周报（不提交）
│   └── .gitkeep
└── README.md
```

## License

MIT
