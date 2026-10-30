# 游戏策划实务即用的 AI · Claude Code 活用法

> 没有一个数字是编造的 —— 一份历时六个月的实战手册：Claude Code、提示词、验证与制作记忆

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](LICENSE)
[![Korean Original](https://img.shields.io/badge/原书-%ED%95%9C%EA%B5%AD%EC%96%B4%ED%8C%90%20(Korean)-blue.svg)](https://github.com/eremes81/game-design-ai-practice)
[![Amazon Kindle (EN)](https://img.shields.io/badge/Amazon%20Kindle-%249.99-FF9900.svg)](https://www.amazon.com/dp/B0H421TWBM)
[![WikiDocs (KR)](https://img.shields.io/badge/WikiDocs-%E5%9C%A8%E7%BA%BF%E5%85%8D%E8%B4%B9%E9%98%85%E8%AF%BB%20(%E9%9F%A9%E8%AF%AD)-1f8b4c.svg)](https://wikidocs.net/book/20216)

**📖 网页版阅读：** [https://eremes81.github.io/game-design-ai-practice-zh-hans/](https://eremes81.github.io/game-design-ai-practice-zh-hans/)

**🌐 各语言版本：** [한국어 — 原书](https://github.com/eremes81/game-design-ai-practice) · [English](https://github.com/eremes81/game-design-ai-practice-en) · [日本語](https://github.com/eremes81/game-design-ai-practice-ja) · [ไทย](https://github.com/eremes81/game-design-ai-practice-th) · [Bahasa Indonesia](https://github.com/eremes81/game-design-ai-practice-id) · **简体中文** · [繁體中文](https://github.com/eremes81/game-design-ai-practice-zh-hant)

📢 The author's second book, 『직장인을 위한 AI 업무 설계의 기술』 (Hanbit Media, Korean) — the author interview is out (in Korean) → https://www.youtube.com/watch?v=v8ygfpAAVQM

> 🧰 **配套工具 — [Harness Starter Kit（骨架工具包）](https://github.com/eremes81/harness-starter-kit)**
> 把本书 1.3（记忆·权限·设置）、第21部分（自我改进）、第24部分（运营）中搭建的**记忆、钩子与复盘结构**打包成可直接运行的最小构成，下载整个文件夹用 AI 代理打开即可。
> 它原本是作者另一本书（面向一般职场）的附录，但骨架与这里讲的是同一套。MIT 许可。


<img src="assets/cover.svg" alt="封面" width="320">

这是一位在游戏行业深耕 24 年的策划总监所写的实战手册，讲的是如何把生成式 AI（Claude Code）真正带进**每天的制作工作**。不是理论，也不是预测——它一次只推进一项任务，从最初的那块屏幕（安装、账号、计费）开始，一路走过系统设计、战斗、叙事、关卡设计、数值平衡、UX，直到长期运营，再到把会议记录变成决策、用验证关卡守住质量、成本管理与版权。

副标题——**「没有一个数字是编造的」**——是这本书的承诺。正文里的每一个数字、每一个案例都来自真实的工作，而不是编造的示例；而且大部分代码仅凭 Python 标准库就能原样跑起来。

这本书也向游戏之外的读者敞开。把会议记录变成决策、追溯一个决策的涟漪、用验证关卡守住质量——这些工作流与你的职业无关都成立。每章的「游戏之外的应用」方框就是那座桥，而每章也都带有一节写给独自一人、没有团队者的「单人精简版」。

---

## 🌐 关于本版本

这是韩语原书《게임 기획 실무에서 바로 쓰는 AI·클로드 코드 활용법》（BOOKK，2026 · ISBN 979-11-12-21479-9）的**简体中文版**。

秉持本书「诚实优先」的原则，这里如实说明本版是怎么做出来的：它是**用本书自己的 AI 工作流从韩语原书翻译而来**（在固定术语表约束下由 Claude 辅助翻译），随后由作者本人审阅——而作者并非中文母语者。所有实操记录（worked transcript）都是对原始韩语会话的翻译，**而非用中文重新跑一遍**；未经改动的韩语原文保存在[韩语仓库](https://github.com/eremes81/game-design-ai-practice)。代码语法、标识符、数字与验证值均保持原样不动。

**非常欢迎母语者纠错**——若有某句读起来不对，请提 Issue 或 Pull Request。繁体中文版由本版经 OpenCC（s2twp，台湾用语）转换派生。

---

## 📖 从这里开始读

- **[序 · 如何阅读本书](manuscript/_front-matter.md)** —— 先看这里，了解各条阅读路线
- **[1.0 开始之前 —— 安装、账号、计费与终端生存包](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)** —— 从最初的那块屏幕跟着走
- 图表以 ` ```mermaid ` 代码块书写，**在 GitHub 上原生渲染**。点开下面任意一章即可阅读。

## 韩语纸质原版

| | |
|---|---|
| 作者 | 李旼洙（이민수）、赵智熙（조지희） |
| 审校 | 赵智熙（조지희） |
| 出版 | BOOKK · 平装（韩语） |
| ISBN | 979-11-12-21479-9 |
| 出版日期 | 2026-06-11 |
| 规格 | 876 页 · 24 部分 + 附录 A–N + 后记 |
| 购买 | **[Amazon Kindle（英文版）$9.99](https://www.amazon.com/dp/B0H421TWBM)** |

本仓库是同一本书的**简体中文版（Markdown 源文）**，按下述许可协议发布。韩语原书在 [eremes81/game-design-ai-practice](https://github.com/eremes81/game-design-ai-practice)。

## 完整目录

> **24 部分 + 附录 A–N + 后记 · 100 章。** 附录在 [`manuscript/part99-appendix/`](manuscript/part99-appendix)，版权页在 [`manuscript/_colophon.md`](manuscript/_colophon.md)。

### 第1部分 · 基础

- [1.0 开始之前 —— 安装·账号·费用·终端生存包](manuscript/part01-foundation/chapter-0-setup-survival-kit.md)
- [1.1 游戏策划与 Claude Code 的第一次相遇](manuscript/part01-foundation/chapter-1-first-encounter.md)
- [1.2 模型·token·驱动框架 —— 一次任务中 token 流动的路径](manuscript/part01-foundation/chapter-2-model-token-harness.md)
- [1.3 记忆·权限·配置基础设施](manuscript/part01-foundation/chapter-3-memory-permission-setting.md)

### 第2部分 · 信息架构

- [2.1 YAML 前置元数据 —— 让所有文档成为数据](manuscript/part02-info-architecture/chapter-4-yaml-frontmatter.md)
- [2.2 按页 Atom —— 单文档单决策的解剖](manuscript/part02-info-architecture/chapter-5-page-atom.md)
- [2.3 Layer 设计 —— 游戏系统抽象化](manuscript/part02-info-architecture/chapter-6-layer-design.md)
- [2.4 本体与 wikilink 图谱 —— 验证语义箭头](manuscript/part02-info-architecture/chapter-7-ontology-graph.md)

### 第3部分 · 系统设计

- [3.1 系统策划的日常与 Layer 坐标](manuscript/part03-system-design/chapter-09-system-designer-and-layer.md)
- [3.2 模式优先 —— $模式比数据更先行](manuscript/part03-system-design/chapter-10-schema-first.md)
- [3.3 关系图可视化 —— 用眼睛看清依赖关系](manuscript/part03-system-design/chapter-11-relation-map.md)
- [3.4 AI 辅助系统设计的提示词模式](manuscript/part03-system-design/chapter-12-ai-assist-prompt-patterns.md)

### 第4部分 · 战斗设计

- [4.1 战斗策划与 Layer —— 打击感落在哪一格](manuscript/part04-combat-design/chapter-13-combat-designer-and-layer.md)
- [4.2 战斗 Look & Feel —— 把手感转化为数值的环节](manuscript/part04-combat-design/chapter-14-look-and-feel.md)
- [4.3 连招·取消·输入队列 —— 枚举路径并加以验证](manuscript/part04-combat-design/chapter-15-combo-cancel-input.md)
- [4.4 AI 辅助战斗模拟与验证](manuscript/part04-combat-design/chapter-16-ai-combat-simulation.md)

### 第5部分 · 叙事

- [5.1 NarrativeDocs Layer 0\~4 结构](manuscript/part05-narrative-design/chapter-1-narrative-docs-layers.md)
- [5.2 世界观 → 角色 → 任务 的一致性验证](manuscript/part05-narrative-design/chapter-2-consistency-verification.md)
- [5.3 AI 辅助叙事写作](manuscript/part05-narrative-design/chapter-3-ai-assisted-narrative.md)
- [5.4 台词·语音一致性](manuscript/part05-narrative-design/chapter-4-dialogue-voice-consistency.md)

### 第6部分 · 内容设计

- [6.1 程序化内容生成与 AI —— 两轴交叉的一格](manuscript/part06-content-design/chapter-1-procedural-content-ai.md)
- [6.2 city_hunting_generator —— 4 周内造出 30 座城市](manuscript/part06-content-design/chapter-2-city-hunting-generator.md)
- [6.3 NPC Persona 与 Squad —— 从玩偶博物馆到小社会](manuscript/part06-content-design/chapter-3-npc-persona-squad-pipeline.md)
- [6.4 内容量产工作流 —— 把多个 generator 串成一条产线](manuscript/part06-content-design/chapter-4-content-production-workflow.md)

### 第7部分 · 关卡设计

- [7.1 程序化关卡设计总纲](manuscript/part07-level-design/chapter-1-procedural-level-design-master.md)
- [7.2 BehaviorTree 编辑器 —— 人与 AI 共同编辑并验证 BT json 的实操记录(worked transcript)](manuscript/part07-level-design/chapter-2-behaviortree-editor.md)
- [7.3 副本·野外模式库](manuscript/part07-level-design/chapter-3-dungeon-field-pattern-library.md)

### 第8部分 · 数值平衡

- [8.1 战斗平衡公式 —— 确定性这一规则手册的位置](manuscript/part08-balance-design/chapter-1-combat-balance-formula.md)
- [8.2 用 Machinations 建模经济 —— 用模拟而非开会来控住通货膨胀](manuscript/part08-balance-design/chapter-2-economy-machinations.md)
- [8.3 Damage Simulator —— 规格 DPS 与模拟结果分岔的那一天](manuscript/part08-balance-design/chapter-3-damage-simulator-2008.md)
- [8.4 AI辅助的平衡模拟](manuscript/part08-balance-design/chapter-4-ai-balance-simulation.md)
- [8.5 PvP·竞技平衡 —— 胜率矩阵·匹配·服务器权威](manuscript/part08-balance-design/chapter-5-pvp-competitive-balance.md)

### 第9部分 · UX/UI

- [9.1 把 HUD 截图挂到 lint 上 —— 让 AI 抓出视线偏离与对比度不足的地方](manuscript/part09-ux-ui-design/chapter-1-hud-layout.md)
- [9.2 技能按钮排布 —— AI 生成 3 个布局方案,lint 负责淘汰](manuscript/part09-ux-ui-design/chapter-2-skill-ui-button-column.md)
- [9.3 ArtGuide/06_UI 协作 —— 策划用 md 写，美术团队只看 html](manuscript/part09-ux-ui-design/chapter-3-artguide-ui-collaboration.md)

### 第10部分 · QA

- [10.1 一致性校验 atom —— 守护 30 张表 FK 的 cascade](manuscript/part10-qa-design/chapter-1-integrity-check-atoms.md)
- [10.2 决策验证 3-layer 传感器 —— 人工评审证据的位置](manuscript/part10-qa-design/chapter-2-decision-validation-3-layer.md)
- [10.3 Alpha Gap Report —— 用自然语言给缺口分类,由人排定优先级](manuscript/part10-qa-design/chapter-3-alpha-gap-report.md)

### 第11部分 · 角色·宠物·坐骑

- [11.1 命名规范与技能-美术映射](manuscript/part11-character-pet-mount/chapter-1-naming-and-skill-art-mapping.md)
- [11.2 宠物·坐骑系统 —— 从1种模板到50种实例](manuscript/part11-character-pet-mount/chapter-2-pet-mount-system.md)

### 第12部分 · 美术

- [12.1 AI 美术资产管线 —— 在可逆阶段量产，在不可逆关卡前停下](manuscript/part12-art-direction/chapter-1-ai-art-asset-pipeline.md)
- [12.2 ArtGuide 七大领域(角色·动画·怪物·NPC·VFX·UI·环境)](manuscript/part12-art-direction/chapter-2-artguide-7-areas.md)
- [12.3 规格书 → 概念 → 游戏内资产的流转](manuscript/part12-art-direction/chapter-3-spec-to-asset-flow.md)

### 第13部分 · 数据与 KPI

- [13.1 将数百条自由回答归为主题——聚类交给AI,诊断交给人](manuscript/part13-data-kpi/chapter-1-faq-meta-game-analysis.md)
- [13.2 KPI 定义·追踪 —— 定义由人来做,异常信号诊断交给 AI](manuscript/part13-data-kpi/chapter-2-kpi-definition-tracking.md)
- [13.3 从异常指标到决策 —— AI 提出假设,人做决策](manuscript/part13-data-kpi/chapter-3-data-driven-decisions.md)

### 第14部分 · 移动端

- [14.1 PC HUD 30 种压缩为移动端 10 种 —— 把约束变成规则手册,把压缩交给 AI](manuscript/part14-mobile-platform/chapter-1-mobile-hud-compression.md)
- [14.2 平台差异(iOS / Android / PC)](manuscript/part14-mobile-platform/chapter-2-platform-differences.md)
- [14.3 触摸 / 鼠标输入设计](manuscript/part14-mobile-platform/chapter-3-touch-mouse-input-design.md)

### 第15部分 · 长期运营（Live Ops）

- [15.1 运营总览 —— 活动候选由 AI 组合,规则手册筛除,人来选定](manuscript/part15-live-ops/chapter-1-live-ops-overview.md)
- [15.2 活动·赛季运营 —— 一张模板生成 10 个变体候选,评审只由人来做](manuscript/part15-live-ops/chapter-2-event-season-ops.md)
- [15.3 把100条反馈归为主题——聚类交给LLM,优先级交给人](manuscript/part15-live-ops/chapter-3-user-feedback-cycle.md)

### 第16部分 · 沟通者

- [16.1 战斗 TF 运营 —— 在隔离的工作空间里,只让决策进入正本](manuscript/part16-communicator/chapter-1-taskforce-operations.md)
- [16.2 与其他工种的协作 —— 把外部请求分入三条轨道（3-track）](manuscript/part16-communicator/chapter-2-cross-job-collaboration.md)
- [16.3 一个决定,三种包装 —— 按职能包装产出物的 framing](manuscript/part16-communicator/chapter-3-cross-team-artifact-framing.md)

### 第17部分 · 会议记录

- [17.1 会议记录为何是最大的痛点](manuscript/part17-meeting-notes/chapter-1-concept-and-motivation.md)
- [17.2 从会议纪要中挖掘决策的提取管线](manuscript/part17-meeting-notes/chapter-2-extraction-pipeline.md)
- [17.3 会议分类·图注·同步 —— 让会议记录成为资产的三条主轴](manuscript/part17-meeting-notes/chapter-3-categories-and-sync.md)
- [17.4 把会议记录变成决策数据库 —— AI 自动化的 5 个切入点](manuscript/part17-meeting-notes/chapter-4-ai-meeting-automation.md)

### 第18部分 · 决策与影响

- [18.1 决策追踪系统](manuscript/part18-decision-impact/chapter-1-decision-tracking-system.md)
- [18.2 影响传播·等级分类](manuscript/part18-decision-impact/chapter-2-impact-propagation-classification.md)
- [18.3 决策前后影响追踪工作流 —— 从事前评估到事后验证](manuscript/part18-decision-impact/chapter-3-pre-post-tracking-workflow.md)
- [18.4 文档影响面 grep 工作流 —— 用 impact 提取影响范围](manuscript/part18-decision-impact/chapter-4-doc-impact-grep-workflow.md)

### 第19部分 · 主管与团队领导

- [19.1 把愿景用作决策的评分表 —— 将 decisions/ 中的 26 个决策交给 LLM 检验](manuscript/part19-team-lead/chapter-1-vision-and-delegation.md)
- [19.2 对冲突分类,不让会议中的决策流失——会议领导力的 AI 辅助](manuscript/part19-team-lead/chapter-2-conflict-and-meeting-leadership.md)
- [19.3 AI引入战略与说服管理层——从保守到激进,ROI 绝不加工](manuscript/part19-team-lead/chapter-3-ai-adoption-strategy.md)

### 第20部分 · 团队协作

- [20.1 单人 DD 运营五人份的协作记忆 —— team_memory 系统](manuscript/part20-team-collab/chapter-1-team-memory-operations.md)
- [20.2 团队成员各自的记忆 —— 用户格与共享格的分离](manuscript/part20-team-collab/chapter-2-team-member-memory.md)
- [20.3 策划门户 —— 团队通过浏览器进入的入口](manuscript/part20-team-collab/chapter-3-portal-web.md)
- [20.4 MCP 项目管理 —— 将协作工具与文档连接到 LLM](manuscript/part20-team-collab/chapter-4-mcp-project-management.md)

### 第21部分 · 自我改进

- [Part 21 · 第1章 复盘是一切的起点](manuscript/part21-self-improving/chapter-1-retro-as-origin.md)
- [Part 21 · 第2章. 复盘系统与 atom 晋升 —— 让发现成为永久资产](manuscript/part21-self-improving/chapter-2-retro-system-atom-promotion.md)
- [Part 21 · 第3章. 闭合 self-improving 循环](manuscript/part21-self-improving/chapter-3-closing-the-loop.md)

### 第22部分 · 治理

- [22.1 提示词工程 —— 游戏策划的一页作业指示书](manuscript/part22-governance/chapter-1-prompt-engineering.md)
- [22.2 自信地说谎的同事 —— 用验证关卡拦住幻觉](manuscript/part22-governance/chapter-2-ai-safety-hallucination.md)
- [22.3 AI 成本管理 —— 用代码守住 token 预算](manuscript/part22-governance/chapter-3-ai-cost-management.md)
- [22.4 著作权与伦理 —— 用一套流程闭合产出物的权利、标示与共识](manuscript/part22-governance/chapter-4-copyright-ethics.md)

### 第23部分 · 扩展与未来

- [Part 23 · 第1章. Wrapper·Cascade·Junction 模式](manuscript/part23-extension/chapter-1-wrapper-cascade-junction.md)
- [Part 23 · 第2章 Hermes Agent 引入实录](manuscript/part23-extension/chapter-2-hermes-agent.md)
- [Part 23 · 第3章. 工具策展 —— 用数据裁掉不用的工具](manuscript/part23-extension/chapter-3-tool-curation.md)
- [Part 23 · 第4章. 独自开发的益智游戏 —— Critter Sort 实战记](manuscript/part23-extension/chapter-4-personal-game-dev.md)

### 第24部分 · 运营实战

- [24.1 验证系统 —— 用代码揪出一致性、链接与 stale 问题](manuscript/part24-ops-deep/chapter-1-verification-system.md)
- [24.2 Mermaid 图表自动化 —— 让文档自己画出自己的图](manuscript/part24-ops-deep/chapter-2-mermaid-diagram-automation.md)
- [24.3 Wikilink 与文档层级 —— 连接与分类,检索的两个入口](manuscript/part24-ops-deep/chapter-3-wikilink-and-hierarchy.md)
- [24.4 来源追踪·data lineage](manuscript/part24-ops-deep/chapter-4-source-tracking-data-lineage.md)

### 后记 · 附录

- [后记 —— 从提问框到游戏设计室](manuscript/part99-appendix/epilogue.md)
- [附录 A. 公司 PC 系统详细清单](manuscript/part99-appendix/appendix-A-company-inventory.md)
- [附录 B. 工具借用流程(从公司到个人的通用化)](manuscript/part99-appendix/appendix-B-tool-adoption-procedure.md)
- [附录 C. 权限·设置参考](manuscript/part99-appendix/appendix-C-permissions-settings.md)
- [附录 D. R&D 文档命名与 Frontmatter 标准](manuscript/part99-appendix/appendix-D-naming-frontmatter-standard.md)
- [附录 E. MCP 服务器目录(游戏策划视角)](manuscript/part99-appendix/appendix-E-mcp-server-catalog.md)
- [附录 F. 案例索引（公司 / 个人 PC）](manuscript/part99-appendix/appendix-F-case-index.md)
- [附录 G. 运营脚本案例集](manuscript/part99-appendix/appendix-G-operation-scripts.md)
- [附录 H. 过往工作资料的复用](manuscript/part99-appendix/appendix-H-past-work-reuse.md)
- [附录 I. BehaviorTree 编辑器案例（进阶）](manuscript/part99-appendix/appendix-I-behaviortree-editor.md)
- [附录 J. 缩略语·术语集](manuscript/part99-appendix/appendix-J-glossary.md)
- [附录 K. 移植到其他 LLM·驱动框架(harness)](manuscript/part99-appendix/appendix-K-tool-neutral-porting.md)
- [附录 L. 团队导入 TCO·上手工作表](manuscript/part99-appendix/appendix-L-team-adoption-tco.md)
- [附录 M. 维度向量·嵌入——面向游戏策划的直觉](manuscript/part99-appendix/appendix-M-embedding-intuition.md)
- [附录 N. 教学用 15 周进度表·难度指南](manuscript/part99-appendix/appendix-N-course-syllabus.md)


---

## 许可协议

本作品采用 **[CC BY-NC-SA 4.0](LICENSE)**（署名—非商业性使用—相同方式共享）许可协议。

- 允许在署名原作者（李旼洙 · 이민수、赵智熙 · 조지희）与来源的前提下进行非商业性的分享、翻译与改编。
- 商业性使用需另行获得作者许可。

正文中少数示例位图（如 `char_skill_ui.png`）为无原图的占位符，可能显示为坏图——在正式纸质／PDF 版中这些位置已填入图像。

ⓒ 李旼洙（Minsoo Lee）、赵智熙（Jihee Jo）2026
