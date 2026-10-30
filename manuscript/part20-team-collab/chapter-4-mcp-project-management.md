---
title: "20.4 MCP 项目管理 —— 将协作工具与文档连接到 LLM"
part: 20
chapter: 4
status: v3
version: v3
written: 2026-05-24
author: 이민수, 조지희
ip_check: done
---

# 20.4 MCP 项目管理 —— 将协作工具与文档连接到 LLM

周二上班后不久,9 点 12 分。我还没打开协作工具的看板,就先在 Claude Code 窗口里敲下一行字。

```
显示本周未完成的 P0 任务,按截止临近程度排序
```

停顿了大约 3 秒,答案就出现了。我没有直接打开协作工具,没有翻找仪表盘标签页,也没有给负责人发即时消息。可是一条已经逾期一天的任务被排在了最上面。我这才打开协作工具,只核对了那一张卡片。

这 3 秒是如何造出来的,就是本章的全部内容。关键在于,我们并没有更换工具。项目A 团队仍然使用协作工具(本项目用的是 ClickUp —— 一种管理任务与日程的 SaaS,JIRA、Redmine、Linear 也处在同样的位置)。无论协作工具是什么,本章的流程只需替换工具名称就能照搬。数据表同样放在 SVN 里,决策卡也同样放在门户里。改变的只有一点:LLM 现在能够**亲手打开并查看**这些工具了。这一连接的标准就是 MCP(Model Context Protocol)。

打个比方,这不是在前台再多安排一名新人,而更像是把现有资料室的锁,也为 LLM 打开。资料室没有变。只是多配了一把钥匙而已。

---

## 20.4.1 MCP 究竟连接了什么

MCP 是 LLM 访问外部工具与数据的标准协议。"标准"二字是关键。它不是为协作工具单独造一个适配器、为文档单独造一个、为 git 再单独造一个,而是在 JSON-RPC 这一个约定之上,每个工具把自己暴露为"服务器",LLM 则作为"客户端"向该服务器发起对话。

结构分三块。

<svg viewBox="0 0 760 220" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="13">
  <rect x="20" y="70" width="180" height="80" rx="8" fill="#e8f0fe" stroke="#3367d6" stroke-width="1.5"/>
  <text x="110" y="100" text-anchor="middle" font-weight="bold">MCP 客户端</text>
  <text x="110" y="122" text-anchor="middle">LLM / 用户</text>
  <text x="110" y="140" text-anchor="middle" fill="#555">(Claude Code)</text>

  <rect x="300" y="70" width="160" height="80" rx="8" fill="#fef7e0" stroke="#f9a825" stroke-width="1.5"/>
  <text x="380" y="105" text-anchor="middle" font-weight="bold">协议</text>
  <text x="380" y="128" text-anchor="middle">JSON-RPC</text>

  <rect x="560" y="30" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="55" text-anchor="middle" font-weight="bold">MCP 服务器 —— 协作工具</text>
  <text x="650" y="74" text-anchor="middle" fill="#555">任务检索·查询</text>

  <rect x="560" y="100" width="180" height="55" rx="8" fill="#e6f4ea" stroke="#1e8e3e" stroke-width="1.5"/>
  <text x="650" y="125" text-anchor="middle" font-weight="bold">MCP 服务器 —— 文档</text>
  <text x="650" y="144" text-anchor="middle" fill="#555">决策卡·GDD 查询</text>

  <line x1="200" y1="110" x2="300" y2="110" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="100" x2="558" y2="60" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <line x1="460" y1="120" x2="558" y2="128" stroke="#666" stroke-width="1.5" marker-end="url(#a)"/>
  <defs><marker id="a" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#666"/></marker></defs>
</svg>

服务器会暴露一份"我能做的事"的清单。若是协作工具服务器,就是 `search_tasks`、`get_task`、`update_task` 这样的函数。客户端(LLM)接收用户的自然语言,从中挑出合适的函数来调用,再把返回的 JSON 用自然语言解释出来。当我说"显示 P0 任务"时,LLM 所做的只是调用了 `search_tasks(priority=P0, status=open)` 而已。

这里要先讲清楚一点。本书不讲怎么亲手编写 MCP 服务器。像 ClickUp、JIRA、GitHub 这样,已经有官方或社区 MCP 服务器的工具占绝大多数,所以策划要做的是"安装并连接服务器",而不是"实现协议"。协议本身由 Anthropic 于 2024 年 11 月作为公开标准发布,规范公开在 modelcontextprotocol.io 上。

---

## 20.4.2 实操记录 —— "显示本周 P0"实际要走的路

光靠嘴说"这会自动完成",听起来像魔法。我们把实际的一次操作从头跟到尾。下面就是这样一段实操记录(worked transcript,完整保留、不作删减的真实操作过程记录):在项目A 接入协作工具 MCP 之后,我第一次跑的会话,几乎原样搬来。LLM 的原始输出不做删减,连别扭的地方也保留。

**① 我敲下的提示词(全文)**

```
请在 ClickUp 中把本周截止、未完成的 P0 任务按截止临近程度整理出来。
每一项都附上负责人和距离截止还剩的天数,已逾期的排到最上面。
```

**② Claude 的原始输出(原样)**

```
在 ClickUp 工作区中,按 P0·未完成·本周截止的条件做了查询。
命中 3 条。(已把逾期的排到最上面。)

1. TASK_017  全局冷却代码变更
   负责人:teammate_a / 截止:昨天(−1 天,已逾期)
2. TASK_023  应用 voice_lint v2
   负责人:teammate_b / 截止:明天(+1 天)
3. TASK_031  更新战斗日志 schema
   负责人:teammate_c / 截止:周五(+3 天)

备注:TASK_009(数值表评审)看起来也是 P0,
但它的 status 是 'in review',是否应算作"未完成"我拿不准。
没有纳入 —— 如果需要,请告诉我判定标准。
```

请注意 LLM 主动停下的这个点。`TASK_009` 处于 'in review' 状态,它是否算"未完成",LLM 没有擅自断定,而是反过来问了人。MCP 能准确取回数据,但"要不要把 in review 算作未完成"取决于团队的定义。假如 LLM 擅自做了这个判断,那反而是事故。

**③ 我做的验证·拒绝**

我打开协作工具,只核对了 TASK_017 这一张卡片。确实已经逾期。但按我们团队的标准,TASK_009 这种 'in review' 也要算进未完成。LLM 的分类和我们的规则不一样。于是我拒绝,并重新给出了标准。

**④ 重新请求**

```
我们团队把 'in review' 也算作未完成。请按这个标准重新整理。
今后也一律把 'in review' = 未完成来对待。
```

之后的输出里,TASK_009 排到了第 2 位。最后那句("今后也一律……来对待")只对本次会话生效。如果不想每次都重复同样的规则,可以把这条定义作为 atom 录入 `team_memory` 的 `shared` 槽位,这样从下一次会话起 LLM 就会自动应用(参见 §20.1·§20.2)。

这一次来回说明的事很清楚。MCP 是**准确取回信息的工具**,而**不是替人做判断的工具**。数据是自动的,定义由人给出。一旦模糊了这条边界,自动化就会变成事故。

---

## 20.4.3 五种应用模式

仅仅是查询协作工具,顶多是"检索变方便了一点"而已。MCP 成为协作系统,是在把多个工具串成一条流程的时候。下面按流程来看项目A 中实际运行的五种模式。

<svg viewBox="0 0 800 400" xmlns="http://www.w3.org/2000/svg" font-family="sans-serif" font-size="11">
  <defs><marker id="mcpar" markerWidth="9" markerHeight="9" refX="7" refY="3" orient="auto"><path d="M0,0 L7,3 L0,6 z" fill="#888"/></marker></defs>
  <text x="400" y="20" text-anchor="middle" font-size="14" font-weight="bold">MCP 五种应用模式 —— 每种模式都是一条独立的流程</text>
  <text x="400" y="38" text-anchor="middle" font-size="10" fill="#666">左侧彩色块是模式,右侧白框是该模式所经的步骤(左→右)</text>

  <!-- 패턴 1 자동 보고서 -->
  <rect x="8" y="52" width="118" height="42" rx="6" fill="#e3f2fd" stroke="#1976d2" stroke-width="1.8"/>
  <text x="67" y="70" text-anchor="middle" font-weight="bold" fill="#1565c0">模式 1</text>
  <text x="67" y="85" text-anchor="middle" font-size="10" fill="#1565c0">自动报告</text>
  <rect x="138" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="197" y="69" text-anchor="middle" font-size="10">每天 09 点</text>
  <text x="197" y="83" text-anchor="middle" font-size="10">调度器触发</text>
  <line x1="256" y1="73" x2="266" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="327" y="69" text-anchor="middle" font-size="10">协作工具·git·</text>
  <text x="327" y="83" text-anchor="middle" font-size="10">仪表盘查询</text>
  <line x1="386" y1="73" x2="396" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="457" y="76" text-anchor="middle" font-size="10">LLM 合成报告</text>
  <line x1="516" y1="73" x2="526" y2="73" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="528" y="53" width="118" height="40" rx="4" fill="#fff" stroke="#1976d2"/>
  <text x="587" y="76" text-anchor="middle" font-size="10">门户/即时消息发送</text>

  <!-- 패턴 2 결정→태스크 -->
  <rect x="8" y="120" width="118" height="42" rx="6" fill="#e8f5e9" stroke="#388e3c" stroke-width="1.8"/>
  <text x="67" y="138" text-anchor="middle" font-weight="bold" fill="#2e7d32">模式 2</text>
  <text x="67" y="153" text-anchor="middle" font-size="10" fill="#2e7d32">决策 → 任务</text>
  <rect x="138" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="197" y="137" text-anchor="middle" font-size="10">登记决策卡</text>
  <text x="197" y="151" text-anchor="middle" font-size="9">proposal P####</text>
  <line x1="256" y1="141" x2="266" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="327" y="137" text-anchor="middle" font-size="10">在协作工具中</text>
  <text x="327" y="151" text-anchor="middle" font-size="10">创建任务</text>
  <line x1="386" y1="141" x2="396" y2="141" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="121" width="118" height="40" rx="4" fill="#fff" stroke="#388e3c"/>
  <text x="457" y="137" text-anchor="middle" font-size="10">负责人·截止</text>
  <text x="457" y="151" text-anchor="middle" font-size="10">自动设置</text>

  <!-- 패턴 3 태스크→카드 -->
  <rect x="8" y="188" width="118" height="42" rx="6" fill="#fff8e1" stroke="#f9a825" stroke-width="1.8"/>
  <text x="67" y="206" text-anchor="middle" font-weight="bold" fill="#e65100">模式 3</text>
  <text x="67" y="221" text-anchor="middle" font-size="9" fill="#e65100">任务→卡片(反向)</text>
  <rect x="138" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="197" y="205" text-anchor="middle" font-size="10">协作工具</text>
  <text x="197" y="219" text-anchor="middle" font-size="10">任务完成</text>
  <line x1="256" y1="209" x2="266" y2="209" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="189" width="118" height="40" rx="4" fill="#fff" stroke="#f9a825"/>
  <text x="327" y="205" text-anchor="middle" font-size="10">决策卡</text>
  <text x="327" y="219" text-anchor="middle" font-size="9">execution_log 更新</text>

  <!-- 패턴 4 진행률 분석 -->
  <rect x="8" y="256" width="118" height="42" rx="6" fill="#f3e5f5" stroke="#7b1fa2" stroke-width="1.8"/>
  <text x="67" y="274" text-anchor="middle" font-weight="bold" fill="#6a1b9a">模式 4</text>
  <text x="67" y="289" text-anchor="middle" font-size="10" fill="#6a1b9a">进度分析</text>
  <rect x="138" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="197" y="273" text-anchor="middle" font-size="10">整个季度</text>
  <text x="197" y="287" text-anchor="middle" font-size="10">任务查询</text>
  <line x1="256" y1="277" x2="266" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="327" y="273" text-anchor="middle" font-size="10">LLM 延期</text>
  <text x="327" y="287" text-anchor="middle" font-size="10">模式分析</text>
  <line x1="386" y1="277" x2="396" y2="277" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="257" width="118" height="40" rx="4" fill="#fff" stroke="#7b1fa2"/>
  <text x="457" y="280" text-anchor="middle" font-size="10">季度复盘输入</text>

  <!-- 패턴 5 1:1 사전 자료 -->
  <rect x="8" y="324" width="118" height="42" rx="6" fill="#fff3e0" stroke="#e64a19" stroke-width="1.8"/>
  <text x="67" y="342" text-anchor="middle" font-weight="bold" fill="#d84315">模式 5</text>
  <text x="67" y="357" text-anchor="middle" font-size="10" fill="#d84315">1:1 事前资料</text>
  <rect x="138" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="197" y="348" text-anchor="middle" font-size="10">1:1 会议前 5 分钟</text>
  <line x1="256" y1="345" x2="266" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="268" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="327" y="341" text-anchor="middle" font-size="9">成员任务 +</text>
  <text x="327" y="355" text-anchor="middle" font-size="9">team_memory·活动</text>
  <line x1="386" y1="345" x2="396" y2="345" stroke="#888" stroke-width="1.3" marker-end="url(#mcpar)"/>
  <rect x="398" y="325" width="118" height="40" rx="4" fill="#fff" stroke="#e64a19"/>
  <text x="457" y="348" text-anchor="middle" font-size="10">自动生成事前摘要</text>
</svg>

**模式 1 —— 自动报告。** 每天早上 9 点,调度器抛出触发信号,LLM 就一次性查询协作工具的任务状态、git 提交、仪表盘指标,写出日报。发送目标是门户或团队即时消息工具。这里的"门户"指的是 §20.3 讲过的公司内部门户网页。`server.py`(FastAPI)始终在运行,Claude 编写的 `View_*.html` 在其上工作,所以报告也就自然地作为门户的一个页面叠加上去。

**模式 2 —— 决策 → 自动生成任务。** 登记决策卡(`proposal P####`)后,卡片的 implementation·verification 项就直接变成协作工具里的任务。连负责人和截止都会自动填入。会议上"那就这么定"所敲定的事,不经人手就落成看板上的卡片。

**模式 3 —— 任务 → 决策卡反向引用。** 是模式 2 的反方向。协作工具的任务一旦完成,MCP 就更新对应决策卡的 `execution_log`。"这个决策是否真的被执行了"会被自动追溯。决策与执行被双向绑定(图中的虚线)。

**模式 4 —— 进度分析。** 季度末,一次性拉取该季度的全部任务,分析延期模式。"哪一类任务反复被拖延"成为复盘的输入。

**模式 5 —— 1:1 事前资料。** 1:1 会议前 5 分钟,把该成员的协作工具任务、`team_memory` 槽位、近期活动合成为一份事前摘要。1:1 不再用"上次你在做什么来着?"浪费 5 分钟,而是直接从正题开始。

五种模式的共同点只有一个:**只有在减少留给人手的重复劳动的地方,价值才被回收。** 为了显得酷炫而加上的模式,只会增加运营负担。

---

## 20.4.4 分阶段引入 —— 不要一次全接上

第一天就把五个 MCP 服务器全部连上,是最常见的失败。是有顺序的。

| 阶段 | 做什么 | 时间感 |
|---|---|---|
| 1 | 安装 1 个 MCP 服务器(ClickUp 或 JIRA) | 1\~2 天 |
| 2 | 试点 1 个模式(自动报告) | 约 1 周 |
| 3 | 运营 5 个模式 | 1\~2 个月 |
| 4 | 自研 MCP 服务器(需要特殊工具时) | 1\~3 个月 |

以上时间是以项目A 的中等规模(10\~50 人)团队为准的作者估计,未经验证。它会随团队规模、工具熟悉度而变化。可以确定的是:**大多数团队走到 1\~3 阶段就够了**。第 4 阶段(自研服务器)只有在必须接入市面上没有 MCP 服务器的特殊内部工具时才走。即使不走到那一步,效果的大部分也已被回收。

单独提一句 JIRA 是有理由的。如果说 ClickUp 是团队内部的看板,那么 JIRA 往往是与发行商、外包这类**外部组织共享**的工具。接上 JIRA MCP,就能在每周会议前自动拉取外包看板的进度,提前筛出疑似延期的任务。会议不再从"现状同步"开始,而是从"决策"开始。不过,越是对外共享的工具,下一节的权限·泄露陷阱就压得越重。

---

## 20.4.5 四个陷阱 —— MCP 为何是双刃剑

MCP 是把工具交到 LLM 手里的事。手里握的若是刀,也可能被割伤。

**陷阱 1 —— 权限事故。** 如果 LLM 连 write 权限也握着,就会发生意料之外的变更。一句"整理一下",就把一批任务状态全改掉,便是这种情形。处方很明确:**MCP 服务器从 read-only 起步。** write 只在模式 2·3 这类确有必要的地方开放,而且要在执行前设一道确认关卡再开。前面的实操记录里,LLM 就 'in review' 的分类反过来问人,也是同一种精神 —— 拿不准就停下。

**陷阱 2 —— 数据泄露。** 用 MCP 拉来的公司数据会被发送到外部 LLM API。数值、未公开内容、营收指标都可能原样流出。处方是:对敏感数据改用自托管 LLM,或在 MCP 服务器一端替换为 placeholder 再发出(与本书通篇的 IP 保护原则一致)。

**陷阱 3 —— 依赖暴增。** 把 5 个 MCP 服务器都挂在 critical 路径上,只要一处挂掉,整份早间报告就停摆。处方是:只把核心的 1\~2 个设为 critical,其余分离为辅助。辅助服务器挂掉时,只是那一项空缺,报告本身照常产出。

**陷阱 4 —— API 成本暴增。** 一次 MCP 调用会同时烧掉 LLM 的 token 和外部 API 调用。若把自动报告每 5 分钟跑一次,成本会悄悄膨胀。处方是:给调用频率设 cap,对不常变化的查询结果做缓存。

把四个陷阱归成一句话,MCP 的安全位置就是:**"从 read-only 起步,只把核心设为 critical,过滤敏感数据,给调用设上限"**。

---

## 20.4.6 效果 —— 时间从哪里被回收

这是项目A 在运营 MCP 前后体感到的变化。下面的时间数字是作者的经验估计(未经验证),请不要当作绝对值,而应作为**方向与比例**来读。

| 事项 | 无 MCP | 运营 MCP | 方向 |
|---|---|---|---|
| 日报信息汇总 | 手动 30\~60 分钟 | 自动 \~5 分钟 | 大幅缩短 |
| 工具间信息同步 | 人工手动 | 自动 | 消除手动 |
| 1:1 事前准备 | 10\~15 分钟 | 自动摘要 \~3 分钟 | 缩短 |
| 外包进度掌握 | 只靠会议 | 实时查询 | 常态化 |
| 决策 ↔ 任务关联 | 手动 | 双向自动 | 防止遗漏 |

最大的回收来自"收集信息的时间"。决策与判断依然是人的工作。MCP 减少的是它前面那一段 —— 翻找散落的工具、把信息汇集到一处的简单劳动。本章开头的那 3 秒,正是这个位置。

---

## 20.4.7 第 20 部分收尾

第 20 部分把团队协作系统垒成了四层。

| 章 | 核心 |
|---|---|
| 20.1 | atom 运营 —— 类别分类、季度整理 |
| 20.2 | 团队成员记忆 —— `team_memory` 5 人槽位(leeminsoo·团队成员 A/b/c·shared),共享 vs 个人分离 |
| 20.3 | 门户网页 —— 用 `server.py`(FastAPI)·`build_index.py`·nginx·nssm 常态运行,`View_*.html` 工作 |
| 20.4 | MCP —— 5 种模式·分阶段引入·权限优先 |

这四章不是各自为政的工具,而是一个整体。门户(20.3)是报告叠加的地方,atom 与记忆(20.1·20.2)是 LLM 记住"in review = 未完成"这类团队定义的地方,MCP(20.4)则是把这一切与协作工具、文档连接起来的线路。任何一项被单独拆走,其余各项的价值也会减半。

下一部分讲治理与运营。把工具接到这个程度之后随之而来的安全性、成本、版权、伦理问题,会把本章的这些陷阱提升为团队层面的规则来梳理。

---

### 本章要点

- MCP 是一种不更换工具、只为 LLM 配出既有工具钥匙的标准。
- 数据由 MCP 取回,定义与判断由人给出 —— 这条边界就是安全线。
- 从 read-only 起步、只把核心设为 critical,自动化就不会蔓延成事故。

---

## 20.4.8 动手试试 —— 首次连接 ClickUp MCP

**setup**
1. 安装 ClickUp MCP 服务器(官方或社区),并申请 ClickUp API token。
2. 在 Claude Code 设置中注册 MCP 服务器,但只以 **read-only 作用域** 起步。
3. 确认工作区 ID,把查询范围限定在自己的看板。

**prompt**
```
请在 ClickUp 中把本周截止、未完成的 P0 任务按截止临近程度整理出来。
附上负责人和距离截止还剩的天数,已逾期的排到最上面。
```

**verify**
1. 从输出的任务中挑 1 条,在 ClickUp 中直接打开,核对截止与负责人是否正确。
2. 看 LLM 是否就模糊的条目主动反问 —— 如果没有反问就擅自断定,就把分类标准写明,再让它重做一次。
3. 常用的定义(如 'in review=未完成')作为 atom 录入 `team_memory` 的 `shared`,让它在下一次会话自动应用。

### 单人精简版

如果你是既没有团队、也没有协作工具的单人开发者,MCP 的第一个对象是 **GitHub 与本地文档**。把 GitHub MCP 以 read-only 接上,从"本周未关闭的 issue,按由旧到新排序"这类查询开始;不用决策卡,而是用文档 MCP 查询本地 `decisions/` 文件夹里的 Markdown。自动报告(模式 1)照样适用 —— 只需把发送目标从团队即时消息换成自己的笔记文件即可。权限·成本陷阱对单人也一样存在,所以最好从一开始就守住 read-only 起步和调用 cap。
