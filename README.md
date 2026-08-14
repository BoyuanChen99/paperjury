<p align="center">
  <img src="docs/paperjury-mark.png" width="170" alt="PaperJury logo">
</p>

<h1 align="center">PaperJury</h1>

<h3 align="center">Due-Process Review for Bounded LaTeX Revision</h3>

<p align="center">
  <b>真正投稿前,先让 AI reviewer 把该挑的坑挑出来。</b><br>
  <b>模型只负责读和想;落槌和改稿的权力,在确定性代码手里。</b>
</p>

<p align="center">
  <a href="https://spark-to-paper-skills.github.io/paperjury/"><img alt="Website" src="https://img.shields.io/badge/Website-paperjury-b07d2a?logo=githubpages&logoColor=white"></a>
  <a href="https://arxiv.org/abs/2606.16322"><img alt="arXiv" src="https://img.shields.io/badge/arXiv-2606.16322-b31b1b?logo=arxiv&logoColor=white"></a>
  <a href="samples/dogfood/"><img alt="Dogfood sample" src="https://img.shields.io/badge/Sample-Dogfood-2f7d55"></a>
  <a href="https://github.com/Spark-To-Paper-Skills/paperjury/releases"><img alt="Releases" src="https://img.shields.io/badge/Releases-stable-3b3d47"></a>
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-yellow.svg"></a>
  <a href="https://github.com/Spark-To-Paper-Skills/paperjury"><img alt="GitHub" src="https://img.shields.io/badge/GitHub-paperjury-181717?logo=github"></a>
</p>

<p align="center">
  <b>中文</b> · <a href="README.en.md">English</a>
</p>

<p align="center">
  <a href="https://spark-to-paper-skills.github.io/paperjury/?lang=zh">🏛️ 项目主页</a> ·
  <a href="https://spark-to-paper-skills.github.io/paperjury/overview.html?lang=zh">🧭 交互式总览</a> ·
  <a href="docs/showcase/SHOWCASE.md">🏆 Dogfood showcase</a> ·
  <a href="docs/AGENT-GUIDE.md">🧑‍✈️ Agent Guide</a> ·
  <a href="CITATION.bib">📌 BibTeX</a> ·
  <a href="https://github.com/Spark-To-Paper-Skills/paperjury-codex">💻 Codex 版</a>
</p>

<p align="center">
  <a href="https://spark-to-paper-skills.github.io/paperjury/?lang=zh">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="docs/overview-card-dark.png">
      <source media="(prefers-color-scheme: light)" srcset="docs/overview-card-light.png">
      <img src="docs/overview-card.png" alt="PaperJury 项目主页" width="100%">
    </picture>
  </a>
</p>

---

<table>
<tr>
<td width="18%">
<a href="docs/showcase/SHOWCASE.md"><img src="docs/paperjury-mark.png" width="120" alt="PaperJury dogfood showcase"></a>
</td>
<td valign="middle">
<b>🏆 真实 Dogfood 样例</b><br><br>
一篇真实草稿的一轮完整 auto 模式评审:仓库里放了<b>修改前后 PDF</b>,以及<b>人工核对过的运行报告</b>。先看样例,再决定要不要把自己的论文交给它挑刺。<br><br>
<a href="docs/showcase/SHOWCASE.md"><img src="https://img.shields.io/badge/查看完整样例_→-Before_After_Report-d73a49?style=for-the-badge" alt="查看完整样例"></a>
</td>
</tr>
</table>

---

> [!IMPORTANT]
> PaperJury 是投稿前的自查工具,**不能替代作者的科学判断,也不能替代 peer review**。它不能用来编造实验、伪造结果、添加没有证据支撑的 claim,或掩盖论文局限。遇到需要新实验、缺证据、需要作者私有知识或研究判断的问题,它都会交回作者处理。

---

## ✨ News

- 🎉 **RedNote(小红书)里程碑:** 相关分享已经达到 **3 万浏览**、**1.8k 收藏**。感谢大家转发和收藏,也感谢大家把 PaperJury 推荐给更多正在赶论文、改论文的朋友。
- 📄 **2026-06-15:PaperJury 论文已上 arXiv。** arXiv 页面:[*PaperJury: Due-Process Review for Bounded LaTeX Revision*](https://arxiv.org/abs/2606.16322)(arXiv:2606.16322)。论文系统介绍了「审稿 → 裁定 → 修改 → 复查」这套引擎:哪些事交给确定性脚本,哪些判断交给语义 agent;有争议的问题如何进入审议;不同风险的编辑该上什么护栏。
- 🔔 **2026-06-10:v1.0.0 发布。** 这是第一个稳定版,和 Codex 版 v1.0 对齐。新增软更新提醒:发现新的稳定 tag 时只提示,不打断当前工作。
- 🚀 **2026-06-05:PaperJury 的 Codex 版已经推送。** 入口在这里:[paperjury-codex](https://github.com/Spark-To-Paper-Skills/paperjury-codex)。
- 🧪 **Dogfood sample 已加入。** 仓库里放了一个紧凑的 [dogfood sample](samples/dogfood/):修改前后 PDF,以及人工核对过的运行报告。

## 📌 引用论文

如果 PaperJury 对你的研究或写作流程有帮助,可以引用这篇 arXiv 论文:

```bibtex
@misc{wang2026paperjurydueprocessreviewbounded,
  title={PaperJury: Due-Process Review for Bounded LaTeX Revision},
  author={Yiran Wang and Ruixuan An and Biao Wu and Wenhao Wang},
  year={2026},
  eprint={2606.16322},
  archivePrefix={arXiv},
  primaryClass={cs.CL},
  url={https://arxiv.org/abs/2606.16322},
}
```

同一条目也放在 [`CITATION.bib`](CITATION.bib)。

---

## ⚡ 两条命令装好,开口就能用

在 Claude Code 里安装:

```text
/plugin marketplace add Spark-To-Paper-Skills/paperjury
/plugin install paperjury@Spark-To-Paper-Skills
```

然后在你的论文项目里直接说需求:

```text
审稿,重点看实验和 claim 是否站得住。
```

也可以更日常一点:

```text
把 introduction 这段改紧一些,但不要改变 claim。
```

不需要背命令。PaperJury 会根据你的描述选择 direct-edit、review 或 auto 模式;真正落稿前,会先把补丁交给你确认。

---

## 📊 同一批论文、同一套口径,数字说话

12 篇 held-out 论文(Vision / NLP / ML 各 4 篇)、四个 baseline、盲审专家审计([arXiv 2606.16322](https://arxiv.org/abs/2606.16322))。删除线是四个 baseline 中最强的 **LLM-as-judge 循环**:

<table align="center">
<tr>
<td align="center"><sub><b>问题质量 · panel-relative F1 ↑</b></sub><br><s>0.519</s> → <b>0.656</b></td>
<td align="center"><sub><b>审计精度 · P<sub>verified</sub> ↑</b></sub><br><s>0.663</s> → <b>0.847</b></td>
<td align="center"><sub><b>不安全编辑率 · ESVR ↓</b></sub><br><s>0.110</s> → <b>0.025</b>(低 4.4×)</td>
</tr>
</table>

| 方法 | F1 ↑ | Acc<sub>v</sub> ↑ | Acc<sub>r</sub> ↑ | ESVR ↓ | 轮数 K | 每篇小时 |
|---|---:|---:|---:|---:|---:|---:|
| Forward-only 重写器 | n/a | n/a | n/a | 0.240 | 1 | 0.31 |
| LLM 批评器 | 0.446 | n/a | n/a | n/a | 1 | 0.51 |
| LLM-as-judge 循环 | 0.519 | 0.681 | n/a | 0.110 | 3.33 ± 1.07(2/12 触顶) | 2.06 |
| 朴素无界生成器 | 0.459 | n/a | n/a | n/a | 1 | 8.37 |
| **PaperJury(本文)** | **0.656** | **0.887** | **0.913** | **0.025** | **3.08 ± 0.67(0/12)** | **2.47** |

<sub>**F1**:相对专家问题清单的 macro F1;**Acc<sub>v</sub> / Acc<sub>r</sub>**:盲审专家对终局裁定 / 路由决定的一致率;**ESVR**:已应用编辑中违反安全的比例(须与编辑量合读:PaperJury 每篇 13.4 处 vs judge 循环 14.3 处);n/a 表示该方法没有这项能力。逐篇配对比较中,PaperJury 的 F1 在全部 12 篇上胜过每个会出问题清单的 baseline。每篇成本 2.47 小时、6.76M token(朴素生成器 8.37 小时、31.4M)。</sub>

三类裁定的盲审复核一致率:invalid-drop **0.872**、valid-fixable **0.913**、author-required **0.860**;消融实验里,拆掉哪个部件,系统就恰好坏在那个部件的职责上(拆护栏链 → ESVR +0.152;拆庭审 → 裁定一致率 −0.153)。完整表格、图和逐项解读见 [项目主页](https://spark-to-paper-skills.github.io/paperjury/?lang=zh) 和 [论文](https://arxiv.org/abs/2606.16322)。

---

## 🤔 每条意见先过堂,再谈改稿

**PaperJury 以 Claude Code skill 的形式提供**,把投稿前自查组织成一套闭环:**审稿 → 裁定 → 修改 → 复查**。它不会照单全收 AI 反馈,而是让每条意见走完正当程序,终结于三种裁定之一:

| 裁定 | 含义 |
|---|---|
| ✅ **valid-fixable(成立可修)** | 表达不清、claim 过强、结构不顺这类文本问题;不需要补实验,也不会把原意改偏。起草最小补丁,过护栏链后落稿。 |
| 🧑‍💻 **author-required(交回作者)** | 缺实验、缺 ablation、缺数据或证据,必须由作者自己判断。原样交回,绝不代笔。 |
| 🛑 **invalid-drop(不成立,驳回)** | AI reviewer 误读了论文,或者提了不该改的问题。驳回并记录在案。 |

## 🎯 适合谁

| 你现在的情况 | 可以直接这样用 |
|---|---|
| **📝 刚写完初稿** | 让它像 reviewer 一样通读全文,先找最可能影响投稿的问题,并把致命问题和小修小补分开。 |
| **🔍 投稿前最后自查** | 让它检查 claim 是否说过头、实验是否撑得住,以及有没有明显格式风险。 |
| **✍️ 只想改一段话** | 直接说「把这段改紧一点,但不要改变 claim」,它会先起草补丁,等你确认后再改;不会把一处小改扩成整篇重写。 |
| **🔁 想多轮打磨但不想一直盯着** | 明确授权 auto 模式;安全修改可以落稿,高风险问题仍会交回作者决定。 |

## 📦 你会得到什么

| 输出 | 内容 |
|---|---|
| **📋 问题清单** | 每条 reviewer-style 问题都会带证据、位置、判断结果和当前状态;不会把一堆意见直接倒进正文。 |
| **🧩 可审阅补丁** | 只有安全修复会进入最小补丁;高风险改动会先放着,等作者决定。 |
| **🛠️ 复查报告** | 有 LaTeX 工具链就真实编译;没有就明说哪些检查做不了,不会假装验证过。 |
| **🧪 真实样例** | [`samples/dogfood/`](samples/dogfood/) 里有修改前后 PDF 和人工核对过的运行报告。 |

它和一般写作工具的差别:

| | 它做的事 |
|---|---|
| **⚖️ 天生对抗式** | N 位领域 reviewer 通读全文 → 可争议性路由把真正的争议送进双方对审的庭审 → 5 人陪审团隔离审议(没有明显多数才升到 12 人)→ 法官给出三种裁定之一。裁定可以是「不修」——顺着你说的改写器,天生给不出这个答案。 |
| **🔁 闭环,不是单向改写** | 每一轮都对改后的稿子干净复查(评审团看不到上一轮的 ledger,再次提出的问题是相互印证,不是锚定效应);确定性书记官把每轮汇入同一本账,直到有一轮再也挖不出新问题为止。落稿之前,还有一批新的质疑者专门找回被误驳回的问题。 |
| **🛡️ 有护栏,不是自动驾驶** | 安全修复在按风险分级的保护下落稿(冻结锚点、单段编辑上限、锚点与跨节含义审计),而且始终等你确认;高风险改动不会悄悄应用,排队等人工过一遍。 |
| **🛠️ 真编译,不止批评** | 在你机器上真实跑 LaTeX 编译,报出真实报错、未定义引用、overfull box 和页数;没有工具链就诚实降级为结构 lint。确定性桌拒检查覆盖经典雷区:匿名化泄漏、页边距魔改、documentclass 漂移、缺必备章节、超页。 |

## 🧭 改一处 → 直接说;想被挑刺 → 说「审稿」;想无人值守 → 用 `/goal`

| 模式 | 什么时候用 | 行为 | 人工确认 |
|---|---|---|---|
| **✍️ direct-edit**(常用) | 只想改一处文字、caption、LaTeX 表达或段落结构。 | 不开评审面板,直接用写作工具包起草补丁。 | 作者确认后再应用。 |
| **🔎 review**(偶尔) | 想让它审稿、挑问题、mock-review,或只审某一节 / 某条 claim。 | 启动对抗式评审引擎,先判断问题是否成立,再决定要不要修改。 | 每处改动逐一确认。 |
| **🔁 auto**(无人值守) | 已经明确给出 `/goal` 或配置 `mode: auto`,希望它多轮跑到一个可验证目标。 | 先确认 `spine` 和评审分配,再按 bounded-aggressive + edit-safety 策略迭代。 | 先给整体授权;高风险项仍交回作者。 |

> [!WARNING]
> **auto 必须明确开启。** 只打开工具权限再发普通 prompt,只会跑一轮就停,不会进入多轮循环。原因见 [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md) §3。

## 🧪 先看它真跑过一次,再交出你的论文

一篇真实的 21 页草稿、11 个埋好的缺陷、一轮完整的 auto 模式评审:152 条 reviewer 意见去重成 55 个问题——**26 处安全落稿、10 个交回作者、19 条驳回**;改后稿件编译 0 error / 0 warning。

[`samples/dogfood/`](samples/dogfood/)([`original_draft.pdf`](samples/dogfood/original_draft.pdf) · [`revised_draft.pdf`](samples/dogfood/revised_draft.pdf) · [运行报告](samples/dogfood/RUN_REPORT.zh-CN.md))

如果只想确认稿件不会先被格式问题挡住,可以说:

```text
跑一下 submission-readiness / 合规检查。
```

它会做确定性格式筛查,再配合编译驱动的版面检查。

## 🚀 安装

### Claude Code plugin

推荐用 marketplace 路线:

```text
/plugin marketplace add Spark-To-Paper-Skills/paperjury
/plugin install paperjury@Spark-To-Paper-Skills
```

### Clone 成 skill

也可以把仓库 clone 到 Claude Code 读取 skill 的目录:

```bash
# macOS / Linux
git clone https://github.com/Spark-To-Paper-Skills/paperjury ~/.claude/skills/paperjury
```

```powershell
# Windows (PowerShell)
git clone https://github.com/Spark-To-Paper-Skills/paperjury "$env:USERPROFILE\.claude\skills\paperjury"
```

也可以放在 `<项目>/.claude/skills/` 下,只对单个项目生效。

安装后建议检查:

- Claude Code 会通过 `SKILL.md` 自动发现它,skill 名称是 `paperjury`。
- 需要 `node`,因为确定性检查跑在 Node 上。
- LaTeX 工具链可选;真实编译和版面检查会用到,没有时会明说哪些检查做不了。
- 在 skill 目录里运行 `npm run doctor`,可以检查仓库完整性、所需工具和论文文件识别。
- 启动时会对 GitHub 稳定版 release tag 做一次软更新检查;发现新版只提示,不阻塞当前工作。设置 `PAPERJURY_DISABLE_UPDATE_CHECK=1` 可以关闭提醒。更新后请开新会话。

### Claude Code 版和 Codex 版怎么选

| 版本 | 入口 | 适合 |
|---|---|---|
| **Claude Code 版** | 本仓库;Claude Code plugin 或 `.claude/skills/` | 你主要在 Claude Code 里写论文、改 LaTeX、跑 workflow。 |
| **Codex 版** | [paperjury-codex](https://github.com/Spark-To-Paper-Skills/paperjury-codex) | 你主要在 Codex / Codex plugin 环境里跑同一套评审和修订流程。 |

**给 Claude / 编码 agent:** 更深入的驱动说明见 [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md)。里面写了安装、三种模式及触发方式、引擎管线、`auto` 与 `/goal` 的区别,以及并行评审如何启动。

## 常见问题

> **PaperJury 能审 Word(.docx)文件吗?**

能。PaperJury 会把 .docx 一次性转成 Markdown,并明确告诉你转换保留了什么、哪些内容带不过来,比如复杂表格和公式。随后它在这份 Markdown 工作副本上跑完整多轮评审。原始 Word 文件不会被改动。结束后你拿回的是改好的 Markdown 和逐条修改清单;要不要合并回 Word,由你自己决定。你也可以先把论文导出成 `.md` 或 `.tex`,再直接交给它。

> **它会不会擅自改我的论文?**

不会。direct-edit 和 review 模式下,补丁需要你确认后才会应用。auto 模式也必须显式开启,并且会先拿到对核心方向、修订范围和策略的整体授权。

## 深入了解

新用户可以先跳过这一节。想看机制、源码结构或 agent 驱动方式,可以从这里开始:

| 你想了解 | 入口 |
|---|---|
| 结果与方法的可视化 | [项目主页](https://spark-to-paper-skills.github.io/paperjury/?lang=zh) · [交互式总览](https://spark-to-paper-skills.github.io/paperjury/overview.html?lang=zh) |
| 真实运行效果 | [`samples/dogfood/RUN_REPORT.zh-CN.md`](samples/dogfood/RUN_REPORT.zh-CN.md) |
| 怎么驱动 Claude / 编码 agent | [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md) |
| 引擎设计细节 | [`docs/REVIEW_ENGINE_V3_DESIGN.md`](docs/REVIEW_ENGINE_V3_DESIGN.md) |
| 完整协议和状态机 | [`references/review-engine-v3.md`](references/review-engine-v3.md) · [`references/ledger-schema.md`](references/ledger-schema.md) |

<details>
<summary><b>展开机制、架构和项目结构说明</b></summary>

### 引擎原理

PaperJury 把审稿拆成一套有边界的「庭审」流程:先由有限数量的 reviewer 找问题,再把有争议的意见拿出来审议;编辑阶段按风险加护栏,多轮结束时由确定性脚本判断是否收敛。

```text
assign-reviewers → reading-check → coverage-auditor → merge
  → { trial ‖ polish } → recall-audit → drafter
  → { edit-audit | meaning-audit } → clerk
```

能用脚本检查的部分都放在 `scripts/` 里,由 orchestrator 在各个 workflow 之间调用;需要判断语义的问题,则交给相互隔离的 model agents。

<details>
<summary><b>确定性步骤(完整清单)</b></summary>

1. **读稿分解**:把手稿(LaTeX 或 Markdown)切成阅读单元、规范段落列表和稳定段落编号,防止问题锚点漂移。
2. **Word 提取**:把 .docx 一次性转成 Markdown 工作副本,并说明哪些内容保住了、哪些内容可能带不过来;原始 Word 文件不改动。
3. **核心声明**(仅 auto 模式):提取核心 claim,交给作者确认后冻结为配置。
4. **Ledger**:用机器可读的记录保存活跃问题,跨轮次、跨会话都能接上。只要没有仍然阻塞的 major 问题,就视为工具侧完成;author-required 会进入人工待办,不算工具侧未完成。
5. **日志**:编辑历史只追加记录,方便回滚。
6. **补丁应用**:原子性应用编辑,记录日志,必要时可以恢复。
7. **锚点追踪**:定位已冻结的核心 claim;上下文变化时,标出需要重新审计的部分。
8. **交叉引用检查**:编辑前先查改动关键词是否还出现在其他位置;如果出现,就标记为需要语义审计。
9. **段落重新对齐**:每轮结束后,重新对齐被编辑挪动的段落编号,避免问题失去锚点。
10. **编译检查**:尝试真实 LaTeX 编译;无法编译时退到结构检查,并明确说明哪些结果不可验证。
11. **提交合规检查**:用脚本先筛一遍常见提交格式风险。
12. **装机自检**:`npm run doctor`,检查仓库完整性、所需工具和手稿识别。

</details>

<details>
<summary><b>语义步骤(完整清单)</b></summary>

1. **评审员分配**:根据论文研究方向,分配 N 位领域 reviewer。
2. **完整阅读检查**:每位 holistic reviewer 通读全文一遍,列出弱点、原文引文、总体置信度和按节覆盖情况;引不出原文,就视为没有真读。
3. **覆盖审计**:检查哪些 reviewer / section 组合可能被略读。
4. **去重**:合并重复评论,并整理重要性、问题类型和交叉确认情况。
5. **审议(trial)**:对有争议的问题开庭。先由 5 人审议,必要时升到 12 人;法官把成立的问题判定为 `valid-fixable` 或 `author-required`。
6. **润色**:快速路径处理机械性问题和轻微问题;如果判断不稳,就升级回审议。
7. **召回审计(recall)**:找回误判丢掉的问题,并在落稿前抽查强共识 major,防止集体误判。
8. **编辑起草**:对确认可修的问题起草最小改动。
9. **编辑审计 / 含义审计**:检查高风险改动、跨节一致性、冻结锚点和论证链条。
10. **书记官**:汇总本轮结果,合并重复项,整理残留问题,并用确定性规则判断是否收敛。

也支持简化的 3 人评审小组,作为快速路径。

</details>

<details>
<summary><b>三个核心组成:Skill + Workflow + Memory</b></summary>

1. **Skill(入口 + 方法论)**:定义协议、reviewer 分配、共识检查、写作工具包和人工确认规则。详见 `references/review-engine-v3.md`、`references/reviewer-personas.md`、`references/writing-toolkit.md`。
2. **Workflow(并行评审引擎)**:语义步骤以 Workflow 运行,并行生成结果,再做 schema 校验。Workflow sandbox 不能直接访问文件系统,所以确定性检查由 orchestrator 在各个 workflow 之间调用。
3. **Memory(持久状态 + 项目约定)**:`LEDGER.json` 是机器可读的主记录,`LEDGER.md` 是给人看的版本;Claude memory 存放下次会话需要沿用的稳定约定,比如 house style、venue 和 reviewer persona 调校。

Reviewer panel 由 N 位领域 reviewer 组成(默认 3 位,范围 2-4 位),运行时按论文 subfield 分配。所有 reviewer 共享同一个资深 reviewer 的底层要求:严苛、精确、建设性;能区分致命缺陷和可修补的小问题,也能跨 section 推理。某个 reviewer 无法确认时,就退回通用 reviewer;单个失败不会拖垮整个 panel。

</details>

<details>
<summary><b>六条硬规则</b></summary>

1. **未经作者显式确认,绝不改手稿。**
2. **评审者 / 陪审员相互隔离。**
3. **每条可修复问题都有明确修复标准。**
4. **不把内部记录写进被审文本。** 评审日志、修订记录和内部检查结论都是作者侧辅助,绝不进入论文或冻结快照。
5. **分歧先讨论;谈不拢时由人覆盖,并记录原因。**
6. **所有路径和文件配置都在运行时解析,不硬编码。**

</details>

## 架构与隐私

- Workflow sandbox 没有文件系统,也不能启动子进程;所以所有确定性检查都由 orchestrator 在 workflow 之间调用。
- `compile-guard.js` 不会假装验证过:无法真正编译时,就退到结构 lint,并报告 `compiled:null`。
- 提交就绪检查分两部分:A = `compliance-check.js` + 一个语义 agent;B = 复用 `compile-guard.js` 的编译检查,再让模型读取 PDF 做版面复查。

> [!NOTE]
> 你的项目文件、ledger、journal 和 patch 都留在本地论文项目里。PaperJury 自己没有后端或服务器,也就不会把文件上传到 PaperJury 服务器。审稿走的是你自己的 Claude Code session;模型本身仍可能跑在云端,内容如何被处理取决于这套 Claude Code 环境的条款和设置,PaperJury 不会再额外加一层。

## 项目结构

| 路径 | 作用 |
|---|---|
| `.claude-plugin/` | Claude Code marketplace 打包配置。 |
| `workflows/` | 语义阶段:评审分配、覆盖检查、合并、庭审、召回审计、起草和收敛。 |
| `scripts/` | 确定性检查脚本:ledger、journal、apply-patch、anchor-diff、cross-ref、compile-guard、doctor 等。 |
| `references/` | 引擎协议、ledger schema、评审者人格、写作工具和方法论。 |
| `docs/` | 项目主页、交互式总览、设计说明、arXiv 论文 PDF 和 agent 驱动指南。 |
| `samples/dogfood/` | 真实草稿的 before/after PDF 和人工核对过的运行报告。 |
| `tests/` | 确定性脚本和核心状态机测试。 |

</details>

## Roadmap

- [x] **软更新提醒。** 启动时检查有没有更新的稳定版 tag,有就给一条非阻塞提示。
- [ ] **快速版本 / quick mode。** 更快、更省 token 的检查路径;不追求完整庭审深度,先给一轮可用的快速 triage。
- [ ] **按不同会议的审稿口味调整 reviewer persona。** CVPR、ACL、NeurIPS 的 reviewer 关注点并不一样;目标是让评审更贴近各自社区的预期。
- [ ] **基于视觉的版面校验。** 编译、渲染、再检查版面,不只看编译日志。
- [ ] **从 `.cls` / 模板自动识别 venue。**
- [ ] **用更多真实论文做规模化验证。**

<details>
<summary><b>更多文件与路径</b></summary>

- 引擎协议:`references/review-engine-v3.md`
- 自动模式:`references/auto-mode.md`
- 评审者角色、编辑工具、方法论:`references/reviewer-personas.md`、`references/writing-toolkit.md`、`references/methodology.md`
- 账本结构和状态:`references/ledger-schema.md`
- 提交合规:`references/submission-compliance.md`
- 设计说明:`docs/REVIEW_ENGINE_V3_DESIGN.md`
- 脚本:`scripts/`(`decompose`、`extract-docx`、`ledger`、`journal`、`apply-patch`、`anchor-diff`、`cross-ref`、`spine`、`rekey`、`compile-guard`、`compliance-check`、`doctor`)
- 步骤:`workflows/`(`assign-reviewers`、`reading-check`、`coverage-auditor`、`merge`、`trial`、`polish`、`recall-audit`、`drafter`、`edit-audit`、`meaning-audit`、`clerk`、`review-panel`)

</details>

**了解更多:** [`docs/AGENT-GUIDE.md`](docs/AGENT-GUIDE.md)(驱动指南)· [`docs/REVIEW_ENGINE_V3_DESIGN.md`](docs/REVIEW_ENGINE_V3_DESIGN.md)(设计说明)· [项目主页](https://spark-to-paper-skills.github.io/paperjury/?lang=zh)

## 致谢

PaperJury 的 spine 和防漂移设计受 [PaperSpine](https://github.com/WUBING2023/PaperSpine) 启发,尤其是 anchor logic-transfer audit、claim register、minimal-edit 且保持原意的改写策略。PaperSpine 更偏 motivation-driven 的论文起草和改写;PaperJury 借用了其中的 anchoring 思路,以及「可检查步骤交给确定性脚本、判断交给 model agent」的分工,再在此基础上加入对抗式 review 和庭审式裁定流程。

---

## Star History

[![GitHub stars](https://img.shields.io/github/stars/Spark-To-Paper-Skills/paperjury?style=for-the-badge&logo=github&color=f5c542&label=GitHub%20Stars)](https://www.star-history.com/#Spark-To-Paper-Skills/paperjury&Date)

<sub>星标曲线暂停:GitHub 限制了第三方获取 stargazer 数据;仓库装上 [star-history GitHub App](https://star-history.com/blog/github-stargazer-api-restriction) 后自动恢复。</sub>
