# Cursor 对你有什么用（非工程师版）

> 一句话：把「结果是文件、能放进仓库、能靠 PR 验收」的活派给 Cursor Cloud Agent，用手机派、用手机验；本机杂活和日常问答继续留给 Grok Bot / Hermes。Pro+ 只拿来养 Grok Bot 确实浪费，但也别把它当第二个 CoS。

## 先记住三条边界

| 路径 | 能做什么 | 做不到什么 | 你在哪操作 |
|---|---|---|---|
| **Cloud Agent（云端）** | 读你 GitHub 上的仓库（私有仓授权后即可），改文件、写脚本、建工具，最后开一个分支 + PR 给你验收 | **看不到 Mac 上没入库的文件**：下载目录里的 PDF、桌面上的 Excel、Hermes 的本地缓存，它一律不知道 | 手机浏览器 / 电脑浏览器打开 cursor.com/agents |
| **桌面 Cursor** | 直接改你 Mac 上打开的那个文件夹，边聊边改 | 手机不能完整遥控它。你必须坐在电脑前 | Mac 上的 Cursor 应用 |
| **手机** | 派 Cloud Agent、看进度、追加指令、看 PR 改了什么、点接受 | 改本机文件不行；没有编辑器、终端、文件浏览器 | 手机浏览器打开 cursor.com/agents（iOS App 在中国区商店没有，网页版够用） |

两个补充：

- 「先在桌面开始、再挪到云端」这条路存在，但它带走的是对话，不是你本地没保存进仓库的改动。别指望用这招把本地文件偷渡上云。
- 桌面有个 Beta 功能 Remote Control：先在 Mac 上启动一次，Mac 不睡眠不断网，手机才能远程指挥那一个会话。这是例外不是常态，本文默认你不靠它。

## 四个你需要认识的词（不用会 git）

- **仓库（repo）**：一个项目文件夹的云端正式版，比如这个 work-skills。
- **分支（branch）**：Agent 在仓库旁边开的一份草稿副本，改坏了不影响正式版。
- **PR（Pull Request）**：Agent 交上来的「我改了这些，你看要不要」。手机上能逐文件看红绿对比。
- **Merge（合并）**：你点一下「接受」，草稿变正式版。不满意就不点，或者在 PR 下追加一句让它改。

你全程只需要做三件事：写任务、看 PR、决定点不点 Merge。

## 对你有价值的用法

- **维护 work-skills 本身**。skill 是你的生产工具，改 SKILL.md、补模板、统一格式，这类活 Cloud Agent 最顺手，PR 就是验收单。
- **写小脚本，让别人跑**。你负责说清「输入什么、输出什么」，Cloud Agent 把脚本和「怎么跑」说明写进 `scripts/`，回到 Mac 让 Hermes 跑一次。Cursor 写、Hermes 跑，两边额度都省。
- **从零起一个小工具**。cursor.com/agents 里选「Start from scratch」，不需要先有仓库。适合「每周把某几个来源整理成一页」这类重复劳动。
- **把口头流程写成 skill**。你平时怎么看公告、怎么拆年报，讲给它，让它仿照 `skills/bp-read` 的结构落成文件，以后 Codex / Hermes 直接调用。
- **仓库体检**。让它读完整个仓，告诉你哪些 skill 重复、哪些模板没人引用、缺什么。结果是一份报告，不需要 Merge。

共同点：任务有边界、产物是文件、你能用 PR 判断好坏。符合这三条就派给 Cursor。

## 不值得的用法

- **Grok Bot 已经做得好的事**：日常问答、资讯汇总、提醒、闲聊。Cursor 干这个纯烧额度，还多一个窗口。
- **处理 Mac 本地没入库的文件**。Cloud Agent 看不见。为了让它看见而把一堆 BP PDF、持仓表塞进 GitHub 也不划算，还多一层数据外泄面。本地文件继续走 Hermes / Codex CLI。
- **大而模糊的任务**（「帮我搭一个投研系统」）。它会跑偏、烧额度、交上来一个你看不懂也不敢 Merge 的东西。拆成一次一个文件、一个脚本的粒度。
- **在桌面 Cursor 里当聊天软件用**。那和任何 Chat 没区别，且你还得坐在电脑前。
- **用它跑需要私钥、账号密码的活**。Cloud Agent 可以配 Secrets，但你作为非工程师第一阶段别碰，出问题不好收拾。

## 明天就能试的 5 个场景

派活统一用这个模板，四行足够：

```
任务：一句话说清做什么
放哪：写到哪个文件 / 文件夹
Done 标准：怎样算做完（我在 PR 里应该看到什么）
别碰：哪些文件不许改
```

### 1. 给 bp-read 做一次体检

- 任务：检查 `skills/bp-read/` 下所有文件，找出模板与 SKILL.md 描述不一致、链接指向不存在文件、术语前后不统一的地方并修正；不改变 skill 的判断逻辑。
- Done：一个 PR，改动只在 `skills/bp-read/` 内，PR 描述里逐条列「发现了什么、改了什么」，你读一遍能点头。

### 2. 一个「批量抽 PDF 文本」小脚本

- 任务：在 `scripts/` 写一个脚本，输入一个文件夹路径，把里面所有 PDF 抽成同名 `.md` 放到旁边的 `text/` 子文件夹；同时写一份 `scripts/README.md` 说明怎么跑、需要装什么。
- Done：PR 里有脚本和说明；回到 Mac，把 README 里那一行命令原样丢给 Hermes 跑，任意一个 BP PDF 能出 md。跑不通就把报错贴回 PR 让它修。

### 3. 从零起一个「公告速读周报」工具

- 任务：在 cursor.com/agents 选 Start from scratch。让它建一个工具：给一组公告链接或本地 PDF 路径，输出一页 markdown 周报（公司、事项、对你持仓/研究的影响一句话、原文链接）。第一版不要联网抓取，只处理你给的输入。
- Done：一个新仓库，README 说清怎么用，`examples/` 里有一次真实输入和对应输出。

### 4. 把「上市公司公告怎么看」写成 skill

- 任务：你先用手机语音口述一遍自己看公告的顺序、先查什么后查什么、什么信号直接放弃，粘进任务里。让它仿照 `skills/bp-read/SKILL.md` 的结构（名称、描述、核心原则、工作流、输出、常见失误）落成 `skills/announcement-read/SKILL.md`。
- Done：PR 里的 SKILL.md 你读起来像自己会说的话，没有被加进你没说过的步骤；结构与 bp-read 对齐。

### 5. 整仓盘点报告

- 任务：读完整个 work-skills，输出一份 `docs/repo-audit.md`：现有 skill 一览、各自解决什么问题、哪些模板 / 参考文件没有被任何 SKILL.md 引用、建议下一个该补的 skill 是什么。
- Done：一份你十分钟能读完的报告。不满意直接在 PR 下留言让它改，满意再 Merge。

## 额度与安全，两件事

- **Cloud Agent 按所选模型的实际用量计费**，第一次使用会让你设支出上限。先设一个小数字，跑完两三个场景看账单再放开。别开最大上下文窗口，费而不必要。
- **私有仓授权只给需要的仓**。Agent 只能看到你自己有权限的仓库，不会多。第一阶段只授权 work-skills 和新起的工具仓。

## 与现有工具的分工，一句话版

- Grok Bot：想事、问事、催事。
- Hermes / Codex CLI：Mac 上动手，处理本地文件。
- Cursor Cloud Agent：仓库里动手，交 PR。
- 桌面 Cursor：坐在电脑前时才开，用来看 PR 改的东西或做需要眼睛盯着的修改。

## 参考（官方文档）

- Cloud Agent 总览：https://cursor.com/docs/cloud-agent
- 手机端说明：https://cursor.com/docs/cloud-agent/mobile
- 从零开始（Start from scratch）：https://cursor.com/docs/cloud-agent/setup
- 安全与隔离边界：https://cursor.com/docs/cloud-agent/security
- 计划与计费：https://cursor.com/docs/models-and-pricing
