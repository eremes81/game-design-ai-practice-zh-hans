# 附录 D. R&D 文档命名与 Frontmatter 标准

> 公司项目A的 R&D 文档命名与 frontmatter 标准(`_NAMING_FRONTMATTER_STANDARD`)的通用化版本。

---

## D.1 命名标准

### D.1.1 atom

```
<category>_<topic>_<subtopic>.md

示例:
combat_global_cooldown_constant.md
narrative_voice_profile_K_007.md
ui_button_primary_style.md
```

snake_case。类别前缀。

### D.1.2 决策卡

```
D<YEAR>_Q<QUARTER>_<NUMBER>.md

示例:
D2026_Q2_017.md
```

年份、季度、编号。

### D.1.3 会议记录

```
<category>_<YYYY-MM-DD>[_<seq>].md

示例:
95_BattleTF_2026-05-18.md
art_review_2026-05-18_1.md
art_review_2026-05-18_2.md
```

### D.1.4 规格书

```
spec_<topic>.md

示例:
spec_combat_global_cooldown.md
spec_guild_attendance.md
```

### D.1.5 报告

```
report_<period>_<type>.md

示例:
report_W21_alpha_gap.md
report_Q2_user_voice.md
```

---

## D.2 Frontmatter 标准

### D.2.1 atom

```yaml
---
name: combat_global_cooldown_constant
description: 定义战斗系统的全局冷却标准值
type: atom
category: combat
status: active
priority: P0
related_atoms:
  - combat_skill_cooldown_rule
  - combat_healing_skill_cooldown_exception
created: 2026-05-18
last_modified: 2026-05-18
related:
  derives_from: [combat_design_principle]
  affects: [combat_skill_cooldown_rule, ui_skill_cooldown_indicator]
---
```

### D.2.2 决策卡

```yaml
---
decision_id: D2026_Q2_017
title: 战斗全局冷却统一为 0.5 秒
type: system_change
status: active
created: 2026-05-18
created_by: 团队成员 A
approved_by: 李旼洙
scope:
  - combat_system
affected_atoms: [...]
implementation:
  target_build: 2026-05-18
verification:
  layer_1: passed
  layer_2: passed
  layer_3: pending
---
```

### D.2.3 会议记录

```yaml
---
type: meeting_note
category: battle
date: 2026-05-18
attendees: [团队成员 A, 团队成员 B, 李旼洙]
related_atoms: [...]
---
```

### D.2.4 规格书

```yaml
---
title: 公会签到功能规格
type: spec
priority: P1
target_milestone: MS2
---
```

---

## D.3 必填 vs 选填字段

### D.3.1 必填字段

| 文档类型 | 必填 |
|---|---|
| atom | name, description, type, category, status |
| 决策卡 | decision_id, title, type, status, created, scope |
| 会议记录 | type, category, date, attendees |
| 规格书 | title, type, priority |

### D.3.2 选填字段（有则更好）

| 文档类型 | 选填 |
|---|---|
| atom | related, last_modified, priority |
| 决策卡 | rationale, related_decisions, verification |
| 会议记录 | related_atoms, sub_topic |
| 规格书 | target_milestone, related_atoms |

---

## D.4 Lint 自动检查

```bash
# frontmatter_lint.py

for file in glob("**/*.md"):
    fm = parse_frontmatter(file)
    if not fm:
        warn(f"{file}: 缺少 frontmatter")
    
    doc_type = infer_type_from_filename(file)
    required = REQUIRED_FIELDS[doc_type]
    
    for field in required:
        if field not in fm:
            warn(f"{file}: 缺少必填字段 {field}")
```

构建时自动执行。违规触发 alert。

---

## D.5 防止命名冲突

| 领域 | 防止 |
|---|---|
| atom name | 全局 unique |
| 决策 ID | 季度内 unique |
| 会议 ID | 日期 + seq |
| 文件名 | 文件夹内 unique |

命名冲突时自动阻止。

---

## D.6 变更流程

### D.6.1 atom 重命名

```
1. 创建新名称的 atom
2. 将原 atom 的所有 wikilink 更新为新名称(自动)
3. 将原 atom 弃用(deprecated)+ 重定向(redirect)
4. 1 个月后移至 _archive
```

仓促的重命名有损坏资料的风险。

### D.6.2 frontmatter 标准变更

```
1. 提出变更理由(decision 流程)
2. 为所有现有文档编写迁移脚本
3. 更新构建 lint
4. 通知团队
```

---

## D.7 读者参考

本标准基于作者的环境。读者需根据自身环境进行调整。核心在于:

| 核心 | 理由 |
|---|---|
| 命名一致性 | 检索、自动化 |
| Frontmatter 标准 | 工具友好 |
| 必填、选填分离 | 填写负担 ↓ |
| Lint 自动 | 强制标准 |
| 变更流程 | 保护资料 |
