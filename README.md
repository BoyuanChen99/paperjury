**中文** · [English](README.en.md)

<p align="center">
  <img src="docs/paperjury-mark.png" alt="PaperJury logo" width="120">
</p>

<h1 align="center">PaperJury</h1>

<p align="center">投稿前，先让 AI 陪审团审一遍。</p>

<p align="center">
  <a href="https://u7079256.github.io/paperjury/paperjury-paper.pdf"><img alt="阅读论文（PDF）" src="https://img.shields.io/badge/论文-PDF-b31b1b?style=for-the-badge&logo=latex&logoColor=white"></a>
  <a href="https://u7079256.github.io/paperjury/overview.html?lang=zh"><img alt="打开在线交互式总览" src="https://img.shields.io/badge/在线交互式总览-d6a14b?style=for-the-badge&logo=githubpages&logoColor=white"></a>
  <a href="https://github.com/u7079256/paperjury/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/u7079256/paperjury?style=for-the-badge&color=3b3d47"></a>
  <a href="https://github.com/u7079256/paperjury/releases"><img alt="latest release" src="https://img.shields.io/github/v/release/u7079256/paperjury?style=for-the-badge&color=3b3d47"></a>
  <img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-3b3d47?style=for-the-badge">
</p>

<p align="center">
  <a href="https://u7079256.github.io/paperjury/overview.html?lang=zh"><img src="docs/overview-card.png" alt="PaperJury 交互式总览" width="760"></a>
</p>

直接问 AI「我论文怎么样」，通常只会得到两种没用的答案：礼貌夸好，或者漫天挑刺。PaperJury 把这件事改成闭环：审稿、裁定、修改、复查。它会把每个问题分成三类：

- **安全修复：** 表达不清、claim 过强、结构不顺这类文本层面的问题；不需要新实验，也不会让论断漂移。
- **作者处理：** 缺实验、缺 ablation、缺数据或证据，得作者自己判断。
- **不成立：** AI 评审误读了论文，或者提了不该改的问题。

PaperJury 是 Claude Code skill，支持三种模式：direct-edit、review、auto。

> [!IMPORTANT]
> PaperJury 是投稿前的自查流程，**不替代作者的科学判断，也不替代 peer review**。它不能拿来编造实验、伪造结果、加没有证据支撑的 claim，或者掩盖论文局限。凡是需要新实验、缺失证据、作者私有知识或研究层面判断的问题，它都交回作者处理，而不是自动写进论文——三类结果的划分正是为此：该由人拿主意的地方，主意始终在你手里。

---

## 目录

- [能得到什么](#能得到什么)
- [三种模式](#三种模式)
- [真实跑一遍](#真实跑一遍)
- [安装](#安装)
- [常见问题](#常见问题)
- [引擎原理](#引擎原理)
- [架构与隐私](#架构与隐私)
- [Roadmap](#roadmap)
- [致谢](#致谢)

<details>
<summary><b>📰 更新日志</b></summary>

> **📄 2026-06-12：PaperJury 论文出炉。** preprint 在这里：[*PaperJury: Due-Process Review for Bounded LaTeX Revision*](https://u7079256.github.io/paperjury/paperjury-paper.pdf)——把整套「审稿 → 裁定 → 修改 → 复查」引擎完整写成论文：确定性与语义的分工、按可争议性路由、对抗式庭审、按风险分级的编辑护栏。
>
> **🔔 2026-06-10：v1.0.0 发布。** 第一个稳定版本，与 Codex 版的 v1.0 对齐。新增非阻塞的更新提醒：有更新的稳定版 tag 时会给出提示。
>
> **🚀 2026-06-05：PaperJury 的 Codex-first 版本已经推送。** 入口在这里：[paperjury-codex](https://github.com/u7079256/paperjury-codex)。
>
> **🧪 Dogfood sample 已加入：** 本仓库现在包含一个紧凑的 [dogfood sample](samples/dogfood/)：修改前后 PDF，以及人工核对过的运行报告。

</details>

---

## 能得到什么

大多数写作工具只会把论文往前推：起草、润色。它们不会像审稿人那样站到你论断的对立面去较真。PaperJury 就是冲着这个缺口设计的，分四块。

| | 它做什么 |
|---|---|
| **对抗式设计** | N 位领域评审通读全文 → contestability router 把真正有分歧的问题送去双方质证的 trial → 5 位互相独立的评审在隔离下审议（僵局才升到 12 位）→ judge 给出三种裁决之一。能给出「不成立」，是一味迎合的 yes-and 改写工具在机制上做不到的。 |
| **闭环，不是单向前推** | 每一轮都是对改后稿的干净复评（评审看不到上一轮台账，同一问题再次出现是相互印证而非锚定），确定性的书记官把每轮结果归并进同一份台账，直到某一轮不再冒出新问题。任何改动落稿前，新的怀疑者还会先试着救回被错误驳回的问题。 |
| **是护栏，不是自动驾驶** | 安全改动在风险匹配的防护下落地：冻结锚点、限制单段改动次数、复核锚点与跨节语义，而且始终需要你的授权。有风险的改动不会被悄悄写入，而是排队等你过一遍。 |
| **真编译，不只是嘴上批评** | 在你本机真跑一次 LaTeX 构建，报告真实报错、未定义引用、overfull box 和页数；没有工具链时诚实降级为结构性检查。确定性的 desk-reject 检查会抓经典坑：匿名泄漏、页边距和行距的小动作、documentclass 漂移、缺失必需章节、超页。 |

---

## 三种模式

你不用输入命令；说出想要什么，skill 会自己选对模式。

| 模式 | 触发 | 行为 | 人工关卡 |
|---|---|---|---|
| **direct-edit**（常用） | 用中/英描述一处改动，直接改手稿（LaTeX 或 Markdown）。例：「把这段改紧一些」「polish this paragraph」「把我对 intro 的想法写成 LaTeX」 | 不进 review 面板，直接走写作工具包起草补丁 | 作者签字后应用 |
| **review**（偶尔） | 想给论文挑问题：review / 审稿 / 评审 / mock-review；范围 `full`（整篇）或 `passage`（某节/段落/claim） | 跑对抗式庭审引擎（`references/review-engine-v3.md`），挑出真正的弱点并把致命缺陷和小问题分开 | 每处改动逐一签字 |
| **auto**（无人值守） | **仅显式开启**：`/goal` 或配置 `mode: auto` | 先定 `spine` 与评审分配（人工），再按 bounded-aggressive + edit-safety 策略多轮跑到收敛 | 前置整体授权 + 返回队列 |

经验法则：**改一处 → 直接说；想被挑刺 → 说「审稿」；想无人值守 → `/goal`。**

> [!WARNING]
> **auto 绝不会被自动检测，只能显式开启。** 它没有任何运行时信号，要么走 `/goal` 上下文，要么靠项目配置 `mode: auto` 进入。只开 "auto" 工具放行 + 发普通 prompt 只会跑一轮就停，不会循环（原因见 [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md) §3）。

---

## 真实跑一遍

想看它真实的产出，仓库里有一个 dogfood sample：在一篇真实草稿上跑完整多轮评审，附**修改前后 PDF** 和一份**人工核对过的运行报告**。

➡️ [`samples/dogfood/`](samples/dogfood/)（[`original_draft.pdf`](samples/dogfood/original_draft.pdf) · [`revised_draft.pdf`](samples/dogfood/revised_draft.pdf) · [运行报告](samples/dogfood/RUN_REPORT.zh-CN.md)）

确认不会被 desk-reject：跟它说「跑一下 submission-readiness / 合规检查」，它会做确定性格式筛查 + 编译驱动的版面检查。

---

## 安装

它是 Claude Code skill，两种装法。Codex-first 版本在这里：[paperjury-codex](https://github.com/u7079256/paperjury-codex)。

**方式 A：Claude Code plugin（marketplace 路线）。** 在 Claude Code 里：

```text
/plugin marketplace add u7079256/paperjury
/plugin install paperjury@u7079256
```

**方式 B：clone 成 skill。** 把仓库 clone 进 Claude Code 读取 skill 的目录：

```bash
# macOS / Linux
git clone https://github.com/u7079256/paperjury ~/.claude/skills/paperjury
```

```powershell
# Windows (PowerShell)
git clone https://github.com/u7079256/paperjury "$env:USERPROFILE\.claude\skills\paperjury"
```

也可以放在 `<项目>/.claude/skills/` 下，只对单个项目生效。装好后注意：

- Claude Code 会通过 `SKILL.md` 自动发现它，随后以 `paperjury` 出现在 skill 列表里。
- 需要 `node`（确定性检查跑在它上面）；LaTeX 工具链可选（真编译和版面检查会用到，没有时诚实降级）。
- 在 skill 目录里跑 `npm run doctor` 自检：检查仓库完整性、所需工具，以及能否找到你的论文文件。
- 启动时会对 GitHub 稳定版 release tag 做一次软更新检查：有更新就提示怎么更新（重跑 plugin 安装，或 clone 安装直接 `git pull`），连不上就保持沉默继续干活。设 `PAPERJURY_DISABLE_UPDATE_CHECK=1` 可关掉提醒；更新后请开新会话。

**给 Claude / 编码 agent：** 更深入的驱动说明见 [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md)：安装、三种模式及触发方式、引擎管线、`auto` 与 `/goal` 的区别、fan-out 怎么启动，都是写给 agent 读的。想了解内部细节，可以让 Claude 先读这个文件再问。

---

## 常见问题

> **PaperJury 能审 Word（.docx）文件吗？**

能。PaperJury 会把你的 .docx 一次性转成 Markdown，并明确告诉你转换保留了什么、哪些内容带不过来（比如复杂表格和公式），然后在这份 Markdown 上跑完整的多轮评审。你的原始 Word 文件绝不会被改动。结束后你拿回的是改好的 Markdown，外加一份逐条修改清单；要不要合并回 Word 由你自己决定，想合并可以用 pandoc 之类的工具。你也可以自己先把论文导出成 .md 或 .tex，直接交给它。

---

## 引擎原理

引擎把这些环节按「庭审」组织起来：生成端有界（N 个领域评审者，而不是按「单元 × 视角」铺开），审议端按争议程度分流，编辑按风险加护栏，多轮循环由确定性的书记官判定收敛。

```text
assign-reviewers → reading-check → coverage-auditor → merge
  → { trial ‖ polish } → recall-audit → drafter
  → { edit-audit | meaning-audit } → clerk
```

确定性 guards 在 `scripts/` 里，由 orchestrator 侧经 Bash 在各 workflow 调用之间运行（Workflow sandbox 没有文件系统，也没有子进程）。

<details>
<summary><b>确定性步骤（完整清单）</b></summary>

1. **读稿分解**：把手稿（LaTeX 或 Markdown）切成阅读单元、规范段落列表和稳定段落编号（防漂移，也给评审提供局部上下文）。
2. **Word 提取**：把 .docx 一次性转成 Markdown 工作副本，并出一份「保留了什么、丢了什么」的诚实报告；原始 Word 文件绝不改动。
3. **核心声明**（仅 auto 模式）：提取核心声明，获得作者确认，冻结为配置。
4. **账本**：活跃问题状态的机器可读源，跨轮次、跨会话持久化。含 gate 逻辑（没有阻断 gate 的活跃 major 即完成；author-required 不阻断 gate，而是累计进人工队列）。`floor` 子命令是重要性地板（只有 major 级、确认可修的问题进自动改稿）；`mode <ledger> collapse` 把 minor 折叠成摘要，让报告聚焦（完整明细始终在 JSON 里）。
5. **日志**：编辑历史只追加记录，支持回滚。
6. **补丁应用**：原子性应用编辑，记录日志，支持恢复。
7. **锚点追踪**：定位已冻结的核心声明；上下文变动时，标出需要重新审计的部分。
8. **交叉引用检查**：编辑安全性预筛：改动关键词是否也出现在其他位置？如出现，标记为需要语义审计。
9. **段落重链**：每轮结束后，重新对齐被编辑挪动的段落编号，问题不丢锚。
10. **编译检查**：尝试真实 LaTeX 编译；无法编译时降级到结构检查并诚实报告不可验证。
11. **提交合规检查**：确定性的案前筛查。
12. **装机自检**：`npm run doctor`，检查仓库完整性、所需工具和手稿识别。

</details>

<details>
<summary><b>语义步骤（完整清单）</b></summary>

1. **评审员分配**：根据论文研究方向，实例化 N 个领域评审者。
2. **完整阅读检查**：每位 holistic reviewer 通读全文一遍 → 弱点（significance + kind + 逐字引文；引不出原文 = 没真读）+ 一个 overall_confidence + 按节覆盖报告；必要时触发定向重读。
3. **覆盖审计**：反 skim 第 2 层，跨覆盖报告标出被略读的 (reviewer, section) 对。
4. **去重**：合并重复评论，确定性导出重要性、问题类别和交叉确认。
5. **审议（trial）**：对有争议的问题开庭：5 人首层、全文辩护 → 独立陪审员带局部上下文（可按需扩展）→ 确定性 quorum + 一方 >60% 多数裁定；法官给 decided-valid 路由（valid-fixable vs author-required）。只有没有明显多数时才升到 12 人。
6. **润色**：快路径处理机械性问题和轻微问题；如判断错误，升级回审议。
7. **召回审计（recall）**：Mode A 救回被误丢的 charge；Mode B 在落稿前抽检强共识 major，防止共识集体出错。
8. **编辑起草**：对确认的可修复问题起草最小改动。
9. **编辑审计 / 含义审计**：edit-audit 查高风险非锚改动（通顺性 + 跨节一致性）；meaning-audit 是四态的冻结锚 + 论证弧审计。
10. **书记官**：汇总本轮结果，去重残留问题，确定性判定是否收敛。

也支持简化的 3 人评审小组，作为快速路径。

</details>

<details>
<summary><b>三原语：Skill + Workflow + Memory</b></summary>

1. **Skill（入口 + 方法论）：** 协议、reviewer 分配、consensus gate、writing toolkit、人工 gate。详见 `references/review-engine-v3.md`、`references/reviewer-personas.md`、`references/writing-toolkit.md`。
2. **Workflow（fan-out 引擎）：** 语义层、无人居中的步骤以 Workflow 运行（并行 + schema 校验输出）。确定性 guards 由 orchestrator 侧经 Bash 在各 workflow 调用之间运行，因为 Workflow sandbox 没有 fs。
3. **Memory（持久状态 + 习得约定）：**
   - **Ledger**：运行时解析出的 `LEDGER.json` 是机器层的 source of truth，外加一份渲染出的 `LEDGER.md` 视图；由 `scripts/ledger.js` 管理。它是跨轮次、跨会话的活 issue 状态。
   - **Claude memory**：当前项目的 memory，值得下次会话继续沿用的稳定约定（本论文的 house style、venue、persona 调校）。

**Reviewer** 是 N 个领域专家 holistic reviewer（默认 3 个，范围 2-4），运行时按论文 subfield 分配，共享一个资深 reviewer gatekeeper 内核：严苛、精确、建设性；把致命缺陷与可修补小问题分开；能跨 section 推理。某个 slot 无法确认（headless）时退回通用 gatekeeper（一个坏 slot 不拖垮整个 panel），通用回退 lens 为 Theory / Foundations、Empirical / Benchmark、Applied / Systems（无固定次序的倾向，不是固定 slot）。

</details>

<details>
<summary><b>六条硬规则</b></summary>

1. **未经作者显式确认，绝不改手稿。** auto 模式会在前期获得作者对核心方向和修订范围的整体授权，之后基于预设策略应用修改，而不是逐次确认。
2. **评审者 / 陪审员相互隔离。** 每轮都是 fresh eyes：互不通气、无上一轮信息泄漏、也看不到 ledger；靠「控制 prompt 里放什么、不放什么」和「每个 reviewer 型 prompt 里显式写明 ISOLATION」双重保证。
3. **每条可修复问题都有明确修复标准。** 由法官设定，说明一处编辑具体要满足什么。
4. **不向被审文本泄漏。** 评审日志、修订记录和内部检查结论都是作者侧辅助，绝不进入论文或冻结快照。
5. **分歧靠讨论解决，谈不拢再由人 override 覆盖（记录在案），绝不暗地驳回。**
6. **所有路径和文件配置都在运行时解析，不硬编码。**

</details>

---

## 架构与隐私

- Workflow sandbox 没有文件系统，也没有子进程；正因如此，所有确定性 guards 都由 orchestrator 侧经 Bash 在各 workflow 调用之间运行。
- `compile-guard.js` 对不可验证性保持诚实：无法真正编译时，降级到结构 lint，并报告 `compiled:null`。
- 提交就绪检查跨模式，分两部分：A = `compliance-check.js` + 一个语义 agent；B = 复用 `compile-guard.js` 的编译驱动版面循环，配合对 PDF 的 Read。

> [!NOTE]
> 你的项目文件、ledger、journal 和 patch 都留在本地论文项目里。PaperJury 没有自己的后端或服务器，所以不会有任何东西发到 PaperJury 的服务器。审稿走的是你自己的 Claude Code session；模型本身跑在云端，内容到了那边怎么处理，跟随你这套 Claude Code 环境的条款和设置，PaperJury 不会再加一层。

---

## Roadmap

还在路上（规划中，尚未上线）：

- [x] 🔔 **软更新提醒。** 启动时检查有没有更新的稳定版 tag，有就给一条非阻塞的更新提示。
- [ ] **快速版本 / quick mode。** 一条低等待、低 token 消耗的快速路径；不追求完整庭审深度，先给可用的快速 triage。
- [ ] **评审人格带上每个会议 community 的 taste。** CVPR、ACL、NeurIPS 的 reviewer 挑刺口味并不一样；目标是让评审带上各自社区的预期。
- [ ] **基于视觉的版面校验**：编译、渲染、再检查版面（分栏溢出、图表摆放），不只看编译日志。
- [ ] **从 `.cls` / 模板自动识别 venue。**
- [ ] **在更多真实论文上规模化验证引擎。**

<details>
<summary><b>文件与路径速查</b></summary>

- 引擎协议：`references/review-engine-v3.md`
- 自动模式：`references/auto-mode.md`
- 评审者角色、编辑工具、方法论：`references/reviewer-personas.md`、`references/writing-toolkit.md`、`references/methodology.md`
- 账本结构和状态：`references/ledger-schema.md`
- 提交合规：`references/submission-compliance.md`
- 设计说明：`docs/REVIEW_ENGINE_V3_DESIGN.md`
- 脚本：`scripts/`（decompose、extract-docx、ledger、journal、apply-patch、anchor-diff、cross-ref、spine、rekey、compile-guard、compliance-check、doctor）
- 步骤：`workflows/`（assign-reviewers、reading-check、coverage-auditor、merge、trial、polish、recall-audit、drafter、edit-audit、meaning-audit、clerk、review-panel）

</details>

**了解更多：** [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md)（驱动指南）· [`docs/REVIEW_ENGINE_V3_DESIGN.md`](docs/REVIEW_ENGINE_V3_DESIGN.md)（设计说明）· [在线交互式总览](https://u7079256.github.io/paperjury/overview.html?lang=zh)

---

## 致谢

spine 与防漂移设计（anchor logic-transfer audit、claim register、minimal-edit 且保义的改写策略）受 [PaperSpine](https://github.com/WUBING2023/PaperSpine) 启发。PaperSpine 是 motivation-driven 的论文起草与改写 skill，是 forward generate/rewrite 工具，没有对抗 loop；PaperJury 借用它的 anchoring 思路，以及「可检查步骤交给确定性脚本、判断交给 model agent」这一机制，再在其上加了对抗式庭审 review 引擎。

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=u7079256/paperjury&type=Date)](https://www.star-history.com/#u7079256/paperjury&Date)
