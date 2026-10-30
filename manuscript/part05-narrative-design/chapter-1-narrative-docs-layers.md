---
title: "5.1 NarrativeDocs Layer 0~4 结构"
part: 5
chapter: 1
status: v3
version: v3
written: 2026-05-24
author: 李旼洙, 赵智熙
ip_check: done
---

# 5.1 NarrativeDocs Layer 0\~4 结构

走进会议室,白板上有一个角色名字被红笔圈了起来。是个叫金某的 NPC。在一位策划的支线任务里,他是"在主角小时候收养并把他养大的养父";而在另一位策划的主线任务第 3 章里,他却是"背叛主角后离去的旧日同伴"。两份文档都在一个月前通过了审批,两者都已进入了构建。连配音录制的报价都拿到了。

谁都没有错。两位策划都读过世界观文档,也都参考了角色设定。问题在于,同一个角色的设定散落在三个不同的文件里,而其中哪一个才是"真的",谁也无法断言。世界观文档是一整块 70 页的 Word 文件,一搜索,金某出现在十一个地方。哪一行是决定、哪一行是备注,没有任何区分。

那天会议结束后定下来的事情,就是把 NarrativeDocs 拆成五层。本章讲的就是这五层的故事。

---

## 5.1.1 为什么从最抽象的领域开始

把按领域的 Layer 分解先从叙事开始,是有理由的。

叙事最抽象。世界观、情感、基调这类东西落不到数字上。它不像美术或系统那样有"精灵图数量""伤害系数"这种明确的单位。如果连这样抽象的领域都能被干净地分解为 Layer,那么更具体的其他领域自然会用同样的模式解开。这相当于先看难的地方能不能走通。

再者,叙事的接口最多。角色与美术相接,任务与内容、关卡相接,台词与 UX、本地化相接,奖励与系统相接。它处在横跨领域最多的位置,所以 Layer 统合的价值会立刻显现出来。

最后,自然语言产出物的占比最高。因此它也是 AI 辅助作用最大的领域。不过并非所有游戏都以叙事为中心。如果是休闲、街机类型,本章的深度可能会显得过头。即便如此,"把一整块文档拆成 Layer、收窄接口"这一骨架本身,可以原封不动地搬到任何领域。

---

## 5.1.2 五格抽屉

把 NarrativeDocs 分解为五层后的样子如下。愿景(L0)在上,构建·QA(L4)在下,连接各层之间的通道有意收得很窄。

<svg viewBox="0 0 720 520" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif">
  <style>
    .layerbox { rx: 8; }
    .ltitle { font-size: 15px; font-weight: bold; fill: #1a1a2e; }
    .ldesc { font-size: 11px; fill: #444; }
    .iface { font-size: 11px; fill: #b03030; font-style: italic; }
    .owner { font-size: 10px; fill: #2a6; }
  </style>

  <!-- L0 -->
  <rect x="120" y="20" width="480" height="60" rx="8" fill="#fdeaea" stroke="#c0392b" stroke-width="2"/>
  <text x="140" y="44" class="ltitle">L0 愿景 —— "这个世界是什么"</text>
  <text x="140" y="64" class="ldesc">world_premise · narrative_pillar · tone_manifesto  (不变 · 约 4.5 页)</text>
  <text x="560" y="44" class="owner" text-anchor="end">总监·主策</text>

  <!-- arrow L0->L1 -->
  <line x1="360" y1="80" x2="360" y2="108" stroke="#888" stroke-width="2"/>
  <polygon points="360,116 355,106 365,106" fill="#888"/>
  <text x="372" y="100" class="iface">pillar · tone (变更时 L1 重新审查)</text>

  <!-- L1 -->
  <rect x="120" y="116" width="480" height="60" rx="8" fill="#eef2fb" stroke="#2c5fa0" stroke-width="2"/>
  <text x="140" y="140" class="ltitle">L1 系统 —— "如何运作"</text>
  <text x="140" y="160" class="ldesc">faction_system · reputation_model · dialogue_branching_rule · lore_consistency_rule</text>
  <text x="560" y="140" class="owner" text-anchor="end">资深叙事</text>

  <!-- arrow L1->L2 -->
  <line x1="360" y1="176" x2="360" y2="204" stroke="#888" stroke-width="2"/>
  <polygon points="360,212 355,202 365,202" fill="#888"/>
  <text x="372" y="196" class="iface">规则手册·分支策略 (受影响任务自动列表化)</text>

  <!-- L2 -->
  <rect x="120" y="212" width="480" height="60" rx="8" fill="#eef9ee" stroke="#2e8b57" stroke-width="2"/>
  <text x="140" y="236" class="ltitle">L2 内容 —— "发生了什么"</text>
  <text x="140" y="256" class="ldesc">main_quest · side_quest · character_bible · lore_codex  (最厚的一层)</text>
  <text x="560" y="236" class="owner" text-anchor="end">多名策划</text>

  <!-- arrow L2->L3 (narrow!) -->
  <line x1="360" y1="272" x2="360" y2="300" stroke="#b03030" stroke-width="3"/>
  <polygon points="360,308 354,297 366,297" fill="#b03030"/>
  <text x="372" y="292" class="iface">quest_id · npc_id · dialogue_id (仅一列)</text>

  <!-- L3 -->
  <rect x="120" y="308" width="480" height="60" rx="8" fill="#fbf5e9" stroke="#c08a2c" stroke-width="2"/>
  <text x="140" y="332" class="ltitle">L3 数据 —— "机器读取的形态"</text>
  <text x="140" y="352" class="ldesc">quest_table · npc_table · dialogue_id_table · reward_table  (自然语言 0 行)</text>
  <text x="560" y="332" class="owner" text-anchor="end">叙事+数据</text>

  <!-- arrow L3->L4 -->
  <line x1="360" y1="368" x2="360" y2="396" stroke="#888" stroke-width="2"/>
  <polygon points="360,404 355,394 365,394" fill="#888"/>
  <text x="372" y="388" class="iface">表格变更时自动触发 lint</text>

  <!-- L4 -->
  <rect x="120" y="404" width="480" height="60" rx="8" fill="#f2eefb" stroke="#7a4fa0" stroke-width="2"/>
  <text x="140" y="428" class="ltitle">L4 构建·QA —— "能否上线"</text>
  <text x="140" y="448" class="ldesc">narrative_qa_checklist · voice_review_log · localization_status</text>
  <text x="560" y="428" class="owner" text-anchor="end">叙事+QA</text>

  <!-- side note: locked anchor -->
  <line x1="120" y1="50" x2="60" y2="50" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="50" x2="60" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <line x1="60" y1="434" x2="120" y2="434" stroke="#c0392b" stroke-width="1.5" stroke-dasharray="4 3"/>
  <text x="52" y="245" class="iface" text-anchor="middle" transform="rotate(-90 52 245)">L0 每次都作为上下文注入 (生成·验收的锚点)</text>
</svg>

落到文件夹上就是下面这个形态。每个文件名都不是书中抽象出来的名字,而是实际存在于那个文件夹中的文件名。

```
NarrativeDocs/
├── Layer0_Vision/
│   ├── world_premise.md          (世界观前提 —— 不变)
│   ├── narrative_pillar.md       (情感支柱 3 根)
│   └── tone_manifesto.md         (基调·禁忌用语清单)
├── Layer1_System/
│   ├── faction_system.md
│   ├── reputation_model.md
│   ├── dialogue_branching_rule.md
│   └── lore_consistency_rule.md
├── Layer2_Content/
│   ├── main_quest/               (以章为单位)
│   ├── side_quest/
│   ├── character_bible/
│   └── lore_codex/
├── Layer3_Data/
│   ├── quest_table.xlsx
│   ├── npc_table.xlsx
│   ├── dialogue_id_table.xlsx
│   └── reward_table.xlsx
└── Layer4_Build_QA/
    ├── narrative_qa_checklist.md
    ├── voice_review_log.md
    └── localization_status.md
```

重要的一点是,这五层不由一个人负责。每一层的主负责人各不相同,只把相邻两层之间的通道标准化。上图中的红色箭头就是那条通道。尤其是 L2 与 L3 之间的通道,故意画得最窄(粗红箭头),其中的理由后面再看。

用抽屉来比喻,就是一个五格抽屉。第一格里放绝不挪动的世界观一行,第二格里放规则手册,第三格里放正文,第四格里放表格,第五格里放验收日志。格与格之间的通道很窄,通道之上挂着变更通知的铃铛。

---

## 5.1.3 L0 —— 为了让它不变而写得尽量小

L0 不会变。它一变,游戏的身份认同就变了。所以篇幅必须小。小才不会变。

| 文档 | 篇幅 |
|---|---|
| world_premise.md | A4 1.5 页 |
| narrative_pillar.md | A4 1 页 (情感 3 个) |
| tone_manifesto.md | A4 2 页 (基调 + 禁忌用语清单) |

合起来约 4.5 页。这就是 L0 的分量。一旦变重,人们就会害怕变更;一害怕,其他层就开始绕过 L0。绕行一旦开始,L0 就成了一份死文档。

`narrative_pillar.md` 的实际骨架是下面这个样子(内容已抽象化)。

```markdown
---
title: 叙事情感支柱
layer: L0
status: locked
last_updated: 2026-05-18
---

## 1. 对失去之物的怀念
- 玩家在每一章结尾都会失去一样东西。
- 失去的东西不会再回来 (只能通过回想)。

## 2. 义务与自由的冲突
- 所有主要 NPC 都背负着两种义务。
- 玩家的选择只能保全其中一种义务。

## 3. 微小举动的分量
- 比起宏大的英雄行为,微小的善意会带来更大的结果。
```

这三行支柱,决定了它下面数百页的方向。`status: locked` 不只是一个普通标签。L4 的自动检查之一会读取这个标签,使得 locked 文档在 PR 中被修改时,若没有主叙事的批准就无法合并。

---

## 5.1.4 L1 —— 与代码最接近的叙事

L1 可以变更,但成本很大。因为它是规则手册。规则手册改一行,所有遵循该规则的内容都会受到影响。

`faction_system.md` 的骨架如下。

```markdown
---
title: 势力系统
layer: L1
atoms:
  - faction_relation_matrix
  - faction_membership_rule
  - faction_quest_eligibility
---

## 1. 势力概念
N 个势力。每个势力由 (理念、资源、领土) 定义。

## 2. 势力之间的关系
- relation_matrix.json (-3 敌对 ~ +3 同盟)
- 关系变化触发条件: 主线任务决定、声望临界

## 3. 玩家归属规则
- 同时归属最多 2 个 (敌对关系不可同时归属)
- 退出惩罚: 声望 -2,同盟势力 -1
```

请留意 frontmatter 的 `atoms:` 列表。这三个 atom 名称不是普通的备注,而是第 7 部分本体论与第 11 部分关系图所追踪的标识符。当某个任务引用了 `faction_quest_eligibility`,这条规则一旦变更,该任务就会自动出现在受影响列表里。L1 是与游戏代码最接近的叙事产出物,所以要与系统策划结对作业。

---

## 5.1.5 L2 —— 最厚的一层,正文居住的地方

L2 最厚。主线任务、支线任务、角色圣经、传说辞典全都住在这里。先前在会议室里冲突过的"养父 vs 背叛的同伴"金某的真正设定,如今也只以 `character_bible/` 中的一个文件存在。那个文件是单一真相来源,任务只引用它。

主线任务文件夹是下面这个形态。

```
main_quest/
├── chapter_01_awakening/
│   ├── 00_chapter_overview.md
│   ├── 01_quest_a_call_to_arms.md
│   ├── 02_quest_b_first_choice.md
│   └── ...
├── chapter_02_road/
│   └── ...
└── _TEMPLATES/
    └── quest_template.md
```

每个任务文件都遵循 atom 标准格式。

```markdown
---
title: 拿起武器时
layer: L2
type: main_quest
atoms:
  - quest_chapter_01_awakening_a
related:
  affects: [reputation_model, faction_relation_matrix]
  derives_from: [narrative_pillar, world_premise]
  requires: [character_kim, faction_alpha]
  part_of: chapter_01_awakening
---

## 进行阶段
1. ...

## 分支
- 选择 A 方案时: ...
- 选择 B 方案时: ...

## 奖励 (参见 L3)
- reward_table.xlsx → quest_001 行
```

核心是 `related:` 块。在写下 `requires: [character_kim]` 的那一刻,这个任务就声明了它从 character_bible 取用金某的设定,不再在自己的文件里重新定义金某。叙事正文放在 L2,数值奖励放在 L3 表格。两者若放在同一个文件里,每改一行表格都得动到正文,而那样一来翻译键就会错位。

---

## 5.1.6 L3 —— 没有一行自然语言的层

L3 是表格和 ID。一行自然语言句子都进不来。

```
quest_table.xlsx
| quest_id | chapter | type | unlock_level | reward_xp | reward_gold | dialogue_set_id |
|----------|---------|------|--------------|-----------|-------------|-----------------|
| q_001    | ch01    | main | 1            | 500       | 100         | ds_001          |
| q_002    | ch01    | main | 2            | 800       | 150         | ds_002          |
```

连台词也只用 ID 来引用。正文另放在 `dialogue_id_table.xlsx` 里,与翻译键 1:1 映射。连接 L2 与 L3 的通道,只需 `quest_id` 一列就够了。前图中唯独这条通道是粗红箭头,原因正在于此。把接口收窄到一列,是 Layer 分离的核心。通道一宽,两侧就会对彼此知道得太多,改动一侧时另一侧就会跟着崩坏。

---

## 5.1.7 L4 —— 出货关卡

L4 是验收与出货。每当新内容进来,自动·人工检查就会启动。自动检查由脚本来跑。下面这四个是实际挂在 CI 上的 lint。

| 检查 | 工具 |
|---|---|
| 所有 dialogue_id 映射存在 | `dialogue_lint.py` |
| 所有 quest_id 都属于某个 chapter | `quest_lint.py` |
| 奖励合计在各章曲线范围之内 | `reward_curve_check.py` |
| 禁忌用语是否出现 | `tone_lint.py` (基于 L0 tone_manifesto) |

请注意 `tone_lint.py` 直接读取 L0 的 `tone_manifesto.md` 这一点。最上层(不变的愿景)与最下层(出货关卡)通过自动化直接连接在了一起。愿景里写下的禁忌用语,若在上线前夕从正文中被检出,构建就会被拦下。

自动抓不到的东西,由人来看。

| 检查 | 负责 |
|---|---|
| 与 L0 情感支柱契合 | 主叙事 |
| 角色配音一致性 | 角色负责人 + 叙事 |
| 本地化可行性 | 本地化人员 |

自动与人工的边界一旦清晰,验收时间就会变得可预测。"这一章的验收要几天?"也就能答得上来了。

---

## 5.1.8 让 AI 来做 Layer —— 实操记录

到这里为止是结构。然而这个结构真正发挥作用的地方,是在制作新内容时。在一个已经铺好五层的项目里,接到一条支线任务的一句话想法,把它撒进各 Layer 的工作,我让 Claude 做了一遍,这里原样搬出那次真实的会话(实操记录,worked transcript —— 完整保留的真实操作过程记录)。不做摘要,连偏掉的部分和被拒绝的部分都一并收录。

**发出的提示词(全文):**

```
绝对不要违反附上的 L0/L1 上下文,按我们的 Layer 结构来分解。

[narrative_pillar.md 全文 —— 情感支柱 3 个]
[tone_manifesto.md 节选 —— 禁忌用语: "命运"、"预言"、"被选中的人"]
[character_bible/character_kim.md 节选 —— 金: 收养主角的养父,
 寡言,话尾含糊,不直接说出情感]

想法: "金把亡妻的遗物交给玩家的一段简短支线任务。"

L2 任务文件(含 related 块,正文 200 字左右)、L3 quest_table 行和
dialogue_id,还有 tone 违规的自我检查。先只写 L2 然后停下。
```

**Claude 的原始输出(L2):**

```markdown
---
title: 褪色的手帕
layer: L2
type: side_quest
atoms:
  - quest_side_kim_keepsake
related:
  affects: [reputation_model]
  derives_from: [narrative_pillar]
  requires: [character_kim]
  part_of: chapter_02_road
---

## 进行阶段
1. 金悄悄把玩家叫过来。不像平常那样直接说出来意。
2. 递出一块旧手帕。"这个……还是你拿着比较好。"
3. 玩家若问那是什么,金不作答,转头望向窗外。
4. (选择) 接下 / 婉拒。

## 分支
- 接下: 金的声望 +1。之后的章节中解锁 1 次与手帕相关的回想。
- 婉拒: 金点点头,把手帕重新收起。声望无变化。
  手帕永远不再出现。

## 奖励 (参见 L3)
- reward_table.xlsx → quest_side_kim_keepsake 行
```

到这里 Claude 停了下来,并补上了一行。

> "为了体现 L0 支柱第 1 条(失去的东西不会再回来),我让选择'婉拒'时手帕永远消失。不过有一点需要确认。亡妻的设定在 character_kim.md 节选里并不存在。这是我擅自加进去的,可能会与角色圣经冲突。"

**人的验证与拒绝:**

这段输出的基调很准。金的寡言、话尾含糊、不直接说出情感的习惯,都活了下来。也没有禁忌用语。然而最后那条自我检查恰恰点中了真正的问题。金有一位亡妻的设定,哪里都没有。AI 从"遗物"这个词自然地推断出了已故的配偶,但这是在角色圣经里偷偷加入新事实的行为。这正是本章开头会议室里那起事故的种子。

所以我拒绝了。发回了重新请求。

**重新请求:**

```
基调不错。但"亡妻"是圣经里没有的新设定,不能用。
金的过去只确定到"离开故乡时留下了点东西"为止。不要指定
遗物的具体身份,只含糊地改成"很久以前留下的东西"之类。
手帕也是圣经里没有的,所以降到"一块布片"之类。
```

**重新请求后的输出(节选):**

```
2. 递出一块旧布片。"很久以前……我留下了一样东西。
   这个就当是它的一角吧。"
3. 玩家若问那是什么,金不作答,转头望向窗外。
```

这次就接受了。既没有把金的过去重新钉死,又触及了情感支柱第 1 条(失去)。失去的究竟是什么,直到最后都含糊地留着。

这一次会话呈现出来的有两点。第一,只要把 Layer 上下文(L0 支柱 + L1 基调 + L2 圣经)准确注入,AI 就能把基调对得惊人地好。第二,AI 一遇到空白就会煞有介事地填满。当那个填补是圣经里没有的新事实时,抓住它的依然是人。Layer 结构的 `requires: [character_kim]` 告诉了我们"该去看哪里",所以验证者立刻就知道该和哪个文件对照。要是没有结构,就得把 70 页重新翻一遍。

---

## 5.1.9 窄通道之上的通知铃

把五层分开的真正理由,是为了收窄接口。而每一处窄接口都贴上变更检测的自动化。

| 接口 | 流动的是什么 |
|---|---|
| L0 → L1 | pillar、tone (变更时触发 L1 规则手册重新审查) |
| L1 → L2 | 规则手册·分支策略 (变更时受影响任务自动列表化) |
| L2 → L3 | quest_id、npc_id、dialogue_id (仅一列) |
| L3 → L4 | 表格变更时自动触发 lint |

例如在 L1 的 `faction_system.md` 中,把"同时归属最多 2 个"改成"最多 1 个"的 PR 提上去时,关系图会扫过引用了 `faction_quest_eligibility` 的 L2 任务,生成一份受影响列表,并把这份列表自动附加到 PR 评论里。改规则的人不必"约两三次会去查谁受影响",看着评论里附的列表,开个 30 分钟的会就结束了。

核心是这一点。如果只分 Layer 而接口含糊,那就只是隔板多了几块而已。比起 Layer 分离本身,接口的自动化才是本质。

---

## 5.1.10 运营 6 个月,改变了什么

迁移到五层、运行 6 个月之后的测量结果。下面的数值基于作者团队的运营记录,但绝对值只以方向·比率来呈现(作者估算·未经验证)。分离前是凭记忆,分离后是实测,因此并非把同一份资料量了两次,这是一个局限。

| 项目 | Layer 分离前 | Layer 分离后 |
|---|---|---|
| 新策划入职上手 | 3 周 | 1 周 |
| 规则手册变更影响范围掌握 | 开会 2\~3 次 | 自动评论 + 会议 30 分钟 |
| 制作一章新主线任务 | 4 周 | 2.5 周 |
| 上线前一章验收 | 5 天 | 2 天 |
| 本地化遗漏事故 | 每季度 3\~5 件 | 每季度 0\~1 件 |

减少得最明显的是本地化遗漏。随着 dialogue_id 在 L3 与翻译键 1:1 绑定,`dialogue_lint.py` 拦下映射遗漏,"未翻译的台词进入构建"的事故几乎消失了。上手变短也很关键。对新策划可以说"只背 L0 的 4.5 页,你的任务就照 L2 模板填",而不是"把 70 页 Word 全读一遍"。

老实补一句,这个效果并非一蹴而就。第一个季度只贴了一项自动评论,其余都是手工。接口自动化是每个季度增加一项。比起分 Layer,贴自动化花的时间更长。

---

## 5.1.11 更深的理由 —— 通往程序化生成的路

到这里为止是表面的理由。"统一各领域之间的协作语言。"然而还有一个更本质的理由。Layer 分解是使程序化生成成为可能的前提。五层各自对应程序化生成中的一个角色(L0 锚点 → L1 规则手册 → L2 正文 → L3 数值 → L4 关卡),而一旦混成一团,生成器就无法确定从哪里读、写到哪里去而崩溃——这一普遍命题在 §6.6 已整体讨论过。这里只看这个前提在叙事五层之上实际是如何运作的。

在一整块 70 页文档之上,生成算法无法确定从哪里读、写到哪里去。叙事五层正好成了生成流水线的五个阶段——L0 锚点、L1 输入规则、L2 正文堆叠的位置、L3 模拟输入、L4 验证关卡。

前面的实操记录其实已经是这五个阶段的精简版了。把 L0 支柱和 L1 基调作为上下文注入(锚点),在 L2 生成了正文,L3 行随之产出,tone 违规的自我检查模仿了验证关卡。把人一次只让做一个任务的事情,在同样的结构上换成让 generator 量产支线任务,就成了程序化生成。

往更远走,就会这样流动——玩家行为累积 → 世界 BT 节点状态变化(Squad 上层) → NPC 数值变化(声望·关注点·优先级) → NPC 标签+数值即为触发条件 → 在任务云中匹配的任务被触发。任务不是预先全写好,而是带着标签像"悬在空中的云"一样放着,玩家的行为一旦改变 NPC 数值,与触发条件相符的任务就会落下来出现。这个进阶模型会在 5.3 再详细讨论(含流程图)。这里要强调的一点是,所有这些流动都只在五层分解之上才能运作。

反过来,Layer 混在一起的团队走不到程序化生成。一尝试,就会因一致性事故而崩溃。想象一下金某既是养父又是叛徒的那起事故,通过生成器被自动量产出来的样子就明白了。

不过这并不意味着一开始就要完美备齐五格抽屉。第一个季度只分离 L0 一行和 L1 规则手册一本也就够了。分离要循序渐进,接口要收窄。

最后关于时点的一点。Layer 分解本身,是从确定性 PCG(Procedural Content Generation,程序化内容生成)时代就有的分离。新出现的是 LLM 在那个分离之上,把自然语言正文、人设、叙事分支也处理了起来——上面的记录里 AI 配合金的基调写出台词这件事,用 5 年前的规则表是做不到的。这套时点论会在 5.3 再展开。

下一章(5.2)将看到,在这五层之上,`lore_consistency_rule` 如何自动验证世界观→角色→任务的一致性,也就是从结构上拦下金某事故的检查器。

---

## 动手试试 —— 第一次 Layer 分解

假设你从已经有一整块世界观文档的状态开始。

**setup.** 在 NarrativeDocs 文件夹下建立五个空文件夹。从 `Layer0_Vision` 到 `Layer4_Build_QA`。把现有的一整块文档原样留着,从中只挑出"绝对不变的那一行",移到 `Layer0_Vision/narrative_pillar.md`。在 frontmatter 里输入 `status: locked`。让这一个文件不超过 4.5 页。

**prompt.** 制作新内容时,按这个顺序把上下文给 AI。

```
[narrative_pillar.md 全文]
[tone_manifesto.md 禁忌用语]
[相关 character_bible 文件节选]

想法: "<一句话想法>"

不要违反这个上下文,先从 L2 任务文件写起。填好 related 块
(requires/derives_from/affects),圣经里没有的新设定
不要加,需要的话就停下来询问。
```

**verify.** 在输出中要看两点。(1) 实际打开 `requires:` 里写的文件,对照 AI 有没有凭空造出那里没有的事实。(2) 在正文中搜索禁忌用语(有 `tone_lint.py` 就自动,没有就用眼睛)。两者只要有一项被命中就拒绝,并明确指出错在哪里后重新请求。上面记录里拒绝"亡妻"的,正是 (1)。

---

## 5.1.12 单人精简版

如果你是没有团队、独自制作的独立开发者,五层可能看起来过头。两格就够了。

放一张 `vision.md`(L0+L1 合并)、一个 `content/` 文件夹(L2),以及一张电子表格(L3)。QA 不另设一层,而是用在 content 文件 frontmatter 里只写 `requires:` 一行的习惯来代替。每次写新任务时,只把 `requires` 里写的文件重新摊开对照,就能不翻遍 70 页也拦下金某事故。核心不在层的数量,而在"把绝对不变的那一行单独抽出来,每次都先给 AI 看"的习惯。那一行就是上下文锚点,无论是一个人还是中等规模的团队,都从那里开始。

---

### 本章要点

- 最抽象的叙事一旦用 Layer 解开,其他领域就会以同样的模式跟上。
- L0 要小才不变,不变才能成为生成·验收的上下文锚点。
- 比起分 Layer,在窄接口上贴自动化才是本质。
