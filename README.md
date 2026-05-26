# family-record

家庭账本 —— 一个简单的家庭支出记录 CLI 工具，支持按角色记录、查询、汇总家庭日常开支。

## 功能

- **记录支出** - 按家庭成员（角色）记录每笔开销
- **查询记录** - 按角色、月份、年份筛选查看
- **汇总统计** - 按月或按年汇总各角色支出
- **删除记录** - 删除错误记录
- **角色管理** - 查看已有家庭成员列表

## 环境要求

- Python 3.6+
- SQLite3（Python 内置，无需额外安装）

## 使用方法

### 记录支出

```bash
python3 ledger.py add --role 爸爸 --amount 100 --note "买菜"
python3 ledger.py add --role 妈妈 --amount 200 --note "买衣服"
python3 ledger.py add --role 儿子 --amount 50 --note "零食"
```

### 查询记录

```bash
# 查看所有记录
python3 ledger.py list

# 按角色筛选
python3 ledger.py list --role 爸爸

# 按月份筛选
python3 ledger.py list --month 2026-05

# 按年份筛选
python3 ledger.py list --year 2026

# 只看最近 N 条
python3 ledger.py list --limit 10

# 组合筛选
python3 ledger.py list --role 妈妈 --month 2026-05
```

### 汇总统计

```bash
# 按月汇总（当月）
python3 ledger.py summary --month 2026-05

# 按年汇总
python3 ledger.py summary --year 2026
```

年度汇总会以表格形式展示每个角色每月的支出明细。

### 删除记录

```bash
python3 ledger.py delete --id 3
```

### 查看角色列表

```bash
python3 ledger.py roles
```

## 数据存储

数据保存在同目录下的 `ledger.db`（SQLite 数据库），无需配置，开箱即用。

## 项目结构

```
record-family/
├── ledger.py     # CLI 主程序
├── ledger.md     # Claude Code skill 配置（自然语言交互）
├── ledger.db     # 数据库文件（自动生成，已 gitignore）
└── README.md
```

## License

MIT
