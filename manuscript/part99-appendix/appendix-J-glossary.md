---
title: "附录 J. 缩略语·术语集"
appendix: J
status: v3
written: 2026-06-06
author: 이민수, 조지희
version: v3
---

# 附录 J. 缩略语·术语集

本附录将正文中出现的缩略语与本书特有术语汇集于一处。正文会在每个缩略语首次出现处展开说明一次,但若你没有按顺序阅读、或中途遗忘,可在此直接查找。若同一缩略语在不同语境下含义不同,则两种含义均予列出。

本术语集按以下顺序分组:团队规模等级 → 游戏策划文档 → 游戏领域 → 数据·运营 → AI·工具 → UI·无障碍标准 → 文件·格式。先想清楚所查缩略语的性质,便能缩小它所在分组的范围。例如 `DPS`·`TTK` 属于"游戏领域",`KPI`·`DAU` 属于"数据·运营",`atom`·`JIT` 属于"AI·工具"分组。

标注规则有三条:① 一般缩略语同时列出正式名称与中文释义。② 像 `atom`·`Wrapper` 这类仅本书使用的特有术语,在正式名称一栏标注了"(本书特有术语)"。③ 像 `PK`(战争语境的 Player Kill ↔ 数据语境的 Primary Key)这样一个缩略语具有两种含义的情况,正文在首次出现时会一并说明是哪一种,而本表中则两种含义均予列出。

## 团队规模等级

本书不将团队人数固定为某个具体数字,而是用以下三个等级来表示。因为即便是同一种方法,导入的深度也会随团队规模而不同。

| 等级 | 人数标准 | 说明 |
|---|---|---|
| 小规模 | \~10人 | 从单人·业余开发者到个位数规模的团队。通常导入 1\~2 个阶段即已足够 |
| 中规模 | 10\~50人 | 本书运营案例所出自的作者团队所处的区间。标准化·一致性自动化的累积效果开始变得明显的规模 |
| 大规模 | 100+ | 多个部门·多个团队。专用基础设施与专职运营得以成立的规模 |

正文中像"中规模(10\~50人)团队"这样同时标注等级与人数范围的地方,均以本表为准。而在像单人·独自开发这类人数本身具有意义的场合,则不用等级,而直接写出确切的人数。

## 游戏策划文档

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| GDD | Game Design Document | 游戏设计文档。确定了系统·数值·行为的详细规格书 |
| CDD | Concept Design Document | 概念设计文档。GDD 之前阶段的早期策划案(方向·概念) |
| TF | TaskForce | 为短期目标而临时组建的专职团队(例:战斗 TF) |
| DD | Design Director | 设计总监。统筹游戏设计方向的主导角色 |
| RnD | Research and Development | 研究·开发。探索原型·新技法的阶段·组织(例:程序化生成 RnD) |

## 游戏领域

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| NPC | Non-Player Character | 玩家不操控的角色 |
| HUD | Heads-Up Display | 叠加显示在游戏画面上的状态信息(生命值·小地图等) |
| DPS | Damage Per Second | 每秒伤害量 |
| GCD | Global Cooldown | 全局冷却。使用一个技能后,所有技能都会短暂一同锁定的公共等待时间 |
| TTK | Time To Kill | 击杀目标所需的时间 |
| PK | Player Kill | (战争·PvP 语境)玩家之间的战斗·击杀 |
| BT | BehaviorTree | 行为树。将 NPC AI 的行为分支以树形定义的结构 |
| FSM | Finite State Machine | 有限状态机。以状态与转移来定义行为的模型 |
| PCG | Procedural Content Generation | 程序化内容生成。以规则·算法自动生成内容 |
| VFX | Visual Effects | 视觉特效 |
| SFX | Sound Effects | 音效 |
| VA | Voice Actor | 配音演员 |
| RPG / MMORPG | (Massively Multiplayer Online) Role-Playing Game | 角色扮演游戏 / 大型多人在线角色扮演游戏 |
| P2W / P2E | Pay To Win / Play To Earn | 靠付费变强的机制 / 靠游玩获得收益的机制 |
| RMT | Real Money Trading | 游戏资源的现金交易 |

## 数据·运营

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| KPI | Key Performance Indicator | 核心绩效指标 |
| DAU | Daily Active Users | 日活跃用户数 |
| FK | Foreign Key | 外键。指向其他表主键的列 |
| PK | Primary Key | (数据语境)主键。唯一标识一行的列 |
| ROI | Return on Investment | 投资回报(回收) |
| MECE | Mutually Exclusive, Collectively Exhaustive | 相互独立·完全穷尽。不重复、不遗漏地进行划分的分类原则 |
| STT | Speech-to-Text | 将语音转换为文本 |
| VBA | Visual Basic for Applications | Excel 内置的宏语言 |
| SVN | Subversion | 文件版本管理系统 |
| telemetry | (计测数据) | 从游戏构建·运行中自动收集的游玩日志·指标(输入·战斗·流失等)。中文常称"遥测" |

## AI·工具

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| AI | Artificial Intelligence | 人工智能 |
| LLM | Large Language Model | 大型语言模型(ChatGPT·Claude 等的底层基础) |
| JIT | Just-In-Time | 仅在需要的瞬间才插入的方式(本书中指根据输入自动注入相应记忆) |
| MCP | Model Context Protocol | 将 AI 工具与外部服务对接的标准 |
| API | Application Programming Interface | 程序间的调用约定 |
| UE | Unreal Engine | 虚幻引擎 |
| atom | (本书特有术语) | 以 1 决策 = 1 文件固化而成的决策·规则卡片 |
| Wrapper / Cascade / Junction | (本书特有术语) | 常用工具的入口 / 将多项检查一次性打包的工具 / 连接到本体的符号链接 |
| rg | ripgrep | 快速文本检索命令(替代 grep 的 CLI 工具)。用于代码·文档的全量检索 |
| ClickUp | (任务·问题追踪器) | 管理工作·日程的云端协作工具。JIRA·Redmine·Linear 也属同一范畴。通过 MCP 对接,由 AI 查询·更新 |

## UI·无障碍标准

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| UI / UX | User Interface / User Experience | 用户界面 / 用户体验 |
| WCAG | Web Content Accessibility Guidelines | Web 内容无障碍指南(对比度·触控目标尺寸等的合格线) |
| HIG | (Apple) Human Interface Guidelines | 苹果的界面指南 |
| SC | Success Criterion | WCAG 的单项合格标准编号(例:SC 1.4.3) |
| pt / dp / px | point / density-independent pixel / pixel | 屏幕尺寸单位 |

## 文件·格式

| 缩略语 | 正式名称 | 含义 |
|---|---|---|
| YAML | YAML Ain't Markup Language | 便于人阅读的配置·数据标记格式 |
| JSON | JavaScript Object Notation | 数据交换的标记格式 |
| HTML / SVG | HyperText Markup Language / Scalable Vector Graphics | Web 文档 / 矢量图形格式 |
| GLB | GL Transmission Format (Binary) | 3D 模型二进制文件格式 |

---

*像 PK 这样含义随语境而不同的缩略语,正文在首次出现时会一并说明是哪一种。若感到混淆,回到本表查看即可。*
