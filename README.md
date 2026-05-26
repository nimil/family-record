# family-record

家庭账本 —— 一个基于 [Claude Code](https://claude.ai/code) Skill 的智能家庭支出记录工具。

用自然语言记账，告别命令行参数。

## 亮点：Claude Code Skill

本项目的核心是一个 Claude Code Skill（`ledger.md`），它让 Claude 理解你的自然语言输入，自动转换为账本操作。

### 使用方式

在 Claude Code 中直接输入自然语言即可：

```
/ledger 爸爸支出100买菜
/ledger 妈妈花了200买衣服
/ledger 儿子50零食
/ledger 查看最近记录
/ledger 这个月爸爸花了多少
/ledger 2026年汇总
/ledger 删除第3条
```

### Skill 支持的操作

| 意图 | 示例输入 |
|------|---------|
| 记录支出 | `爸爸支出100买菜`、`妈妈花了200买衣服` |
| 查询记录 | `查看最近记录`、`爸爸本月支出` |
| 月度汇总 | `这个月花了多少`、`2026-05 汇总` |
| 年度汇总 | `2026年汇总`、`年度统计` |
| 删除记录 | `删除第3条` |
| 查看角色 | `有哪些角色`、`角色列表` |

Skill 会自动识别意图、解析参数，调用底层 CLI 工具并返回结果。

### 安装 Skill

将 `ledger.md` 放到项目的 `.claude/commands/` 目录下即可：

```bash
mkdir -p .claude/commands
cp ledger.md .claude/commands/
```

之后在 Claude Code 中输入 `/ledger` 即可使用。

## CLI 直接使用

也可以直接通过命令行操作：

```bash
# 记录
python3 ledger.py add --role 爸爸 --amount 100 --note "买菜"

# 查询
python3 ledger.py list --role 妈妈 --month 2026-05

# 汇总
python3 ledger.py summary --year 2026

# 删除
python3 ledger.py delete --id 3

# 角色列表
python3 ledger.py roles
```

## 环境要求

- Python 3.6+
- SQLite3（Python 内置）
- [Claude Code](https://claude.ai/code)（使用 Skill 功能时需要）

## 数据存储

数据保存在同目录下的 `ledger.db`（SQLite 数据库），无需配置，开箱即用。

## 项目结构

```
record-family/
├── ledger.py     # CLI 主程序
├── ledger.md     # Claude Code Skill（自然语言交互核心）
├── ledger.db     # 数据库文件（自动生成，已 gitignore）
└── README.md
```

## License

MIT
