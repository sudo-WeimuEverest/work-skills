---
name: bp-read
description: Read startup BP, pitch deck, or fundraising PDFs and produce an investor-oriented first-pass memo. Use when Codex receives a company presentation or BP and must explain the business clearly from an investment perspective, translate technical claims into commercial and economic consequences, run a light web-based fact pattern check, identify what should be researched next across reports, listed-company filings, announcements, and market data, and recommend which materials deserve a quick skim versus deeper reading.
---

# BP Read

把 BP PDF 转成一套适合投资人首轮阅读的初步判断材料。先提炼公司自己的叙事，再叠加一层轻量外部验证，最后输出 memo 式介绍页、研究优先级和快速精读清单。

所有面向用户的输出默认使用用户当前工作语言。若用户主要用中文，就用中文写正文；涉及公司、产品、公告、法规、财报标题时，保留原始语言以保证准确性。

## 核心原则

- 明确区分 `BP 原始说法`、`外部已验证事实`、`推断判断`，不要混写。
- 保留 BP 原意，只做澄清和重组，不替公司润色。
- 用投资语言解释技术，重点讲清它改变了什么：成本、效率、质量、转化、留存、毛利、合规、部署难度、替代风险。
- 外部验证优先使用一手或准一手来源：官网、产品文档、交易所公告、年报、监管文件、官方数据。
- 第一轮只做首读判断，不默认展开成完整尽调。
- 对不确定性要显式标注。关键问题答不上来，就把它写进后续研究议程。
- 所有面向用户的最终输出，末尾都必须追加 `Sources` section，列出本次结论实际使用过的信息来源，并附可直接打开的网址链接；不要只写站点名，不要省略 URL。

## 工作流

1. 读取 BP PDF。
2. 在外部搜索前，先抽取公司自己的核心叙事。
3. 形成一版内部摘要：问题、产品、商业模式、目标客户、获客路径、进展、融资诉求、关键数字。
4. 找出 BP 里最强的 claim 和最弱的证据支撑，列成验证清单。
5. 做一轮轻量外部搜索，校验基础事实并补齐市场背景。
6. 将技术创新翻译成商业和投资意义。
7. 输出标准结果包。

## BP 首读

在搜索外部信息之前，先完整提炼 BP 自己在说什么。

- 提炼公司的一句话定义。
- 按 BP 的口径写清楚它解决什么问题。
- 拆解方案结构：产品、工作流、技术、数据、渠道。
- 记录变现逻辑：谁付钱、为啥付钱、收入如何放大。
- 抽出所有值得验证的数字：ARR、用户数、试点数、客户数、留存、毛利、部署周期、单元经济、市场规模、定价。
- 标记缺失信息：客户集中度、采购周期、监管约束、毛利天花板、资本开支、对合作方依赖、对补贴或政策依赖。

处理 PDF 时遵循本地 `pdf` skill 的原则：文本提取用于加速理解，但不要仅凭抽取文本就对版式或上下文关系做过度判断。

## 外部搜索

这一轮搜索的目标是“快速建立可信的外围事实框架”，不是做穷尽式尽调。

- 先看官网、产品页、定价页、新闻页、招聘页。
- 再看融资新闻、客户公告、创始人采访、产品发布。
- 再沿产业链搜索潜在客户、供应商、合作方、incumbent 的年报与公告。
- 再看行业报告、协会材料、监管通知、官方统计，验证市场需求和 adoption 约束。
- 当你已经足以修正首轮判断时就停下来。这个 skill 解决的是“优先级排序”，不是一次性写完研究报告。

需要更具体的搜索顺序和 query pattern 时，读取 [search-playbook.md](references/search-playbook.md)。需要判断下一步先搜什么时，读取 [source-priority.md](references/source-priority.md)。

## 技术到投资语言的翻译

不要只复述技术术语，要把技术含义翻译成经济后果。

- 问清它解决了哪个运营瓶颈。
- 问清它到底改善了收入、毛利、留存、转化、合规、吞吐，还是降低了替代风险。
- 问清优势到底来自算法表现、工作流贴合、数据积累、集成深度、硬件成本曲线、监管时点，还是渠道分发。
- 对比的是现有主流替代方案和最可信的 substitute，不只是 BP 里写的竞争对手。

写介绍页时，优先参考 [memo-framework.md](references/memo-framework.md)。

## 输出结果包

除非用户明确要求拆分文件，否则默认输出为 **一个总 `markdown` 文件**，内部按以下四个 section 组织：

1. `Memo Intro` using [memo-intro-template.md](assets/memo-intro-template.md)
2. `Research Priority` using [research-priority-template.md](assets/research-priority-template.md)
3. `Quick Read List` using [quick-read-template.md](assets/quick-read-template.md)
4. `Evidence Table` using [evidence-table-template.md](assets/evidence-table-template.md)

在以上四个 section 之后，必须追加一个 `Sources` section：

- 只列本次分析中实际引用、实际支撑判断的来源，不堆砌无关链接。
- 每条至少包含：来源名称、来源类型（如官网、监管、媒体、论文/项目页、客户公告）、网址。
- 若某条结论仅来自 `BP 原始说法` 且无外部链接，也要在正文中明确写“仅 BP 提及”，但 `Sources` section 不需要为此虚构链接。
- 若用户后续要求更深入版本，仍然保留这个 section，并放在全文末尾。

如果用户明确要求拆分，再分别输出 `memo-intro.md`、`research-priority.md`、`quick-read-list.md`、`evidence-table.md` 四个文件。

这套结果要回答四个问题：

- 这家公司到底做什么，为什么可能值得看？
- 它真正的创新点或非共识点在哪里？
- 下一步最该验证什么？
- 哪些来源最能快速压缩不确定性？

## 优先级判断规则

优先做那些能最快缩小关键不确定性的研究。

- 第一，验证问题是否真实存在，且有人愿意为之付预算。
- 第二，验证方案是否真的优于现有工作流。
- 第三，验证渠道、采购、部署路径是否合理。
- 第四，验证已有进展是否具备可重复性，而不是一次性案例。
- 第五，验证市场结构是否支持足够大的投资回报空间。

如果一个 BP 技术讲得很多，但客户证据很弱，就把后续研究重心放在需求、买方、采购和 adoption 证据上，而不是继续堆技术阅读。

## 常见失误

- 写成了公司介绍稿，而不是投资人首轮判断。
- 把 TAM 页或创始人口径当成事实。
- 讲了创新，却没讲创新带来的商业后果。
- 推荐了一堆泛泛资料，而不是少量最能改变判断的材料。
- 还没提炼 BP 自己的 thesis，就先去广泛搜索。

## 示例触发

- "Use $bp-read on this BP PDF and give me a one-page investor intro plus what to research next."
- "Use $bp-read to explain the company's innovation clearly without losing technical accuracy."
- "Use $bp-read to tell me which reports, announcements, and filings I should read first."
- "Use $bp-read to turn this fundraising deck into an investment memo opening page."

## 参考文件

- Memo framing: [memo-framework.md](references/memo-framework.md)
- Research source order: [source-priority.md](references/source-priority.md)
- Search workflow: [search-playbook.md](references/search-playbook.md)
- Memo template: [memo-intro-template.md](assets/memo-intro-template.md)
- Research template: [research-priority-template.md](assets/research-priority-template.md)
- Quick-read template: [quick-read-template.md](assets/quick-read-template.md)
- Evidence table template: [evidence-table-template.md](assets/evidence-table-template.md)
