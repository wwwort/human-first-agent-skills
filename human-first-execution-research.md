# 让 GPT 说人话：交流方式与决策解放的联合调研

**调研截止：2026 年 10 月 10 日**  
**目标：**在不修改 GPT/Codex 官方模型、系统策略、路由、额度、工具权限和安全边界的前提下，降低交流成本、理解带宽压力和责任转移，并把结论落成可复用的外接 skill。

## 一、结论先行

社区对 Opus 5.5 的高评价，核心集中在一种协作感：它更早给出重要信息，更少写旁枝、术语和“做完之后还有一堆 loose ends”，在长任务里更容易跟随。社区把这种体验描述成“像在和成年人或同事交流”，但真正可迁移的部分是信息顺序、相关性、自然承接、有限的澄清和对结果负责。

GPT/Codex 的反感点与能力强弱并不完全重合。大量抱怨指向可见交互：企业腔、模板化赞美、过度谨慎、简单任务反复确认、权限与 handoff 噪声、把普通选择推回用户、任务尚未完成就结束、每轮在尾巴追加“如果你愿意我可以……”。这些行为把模型本来应该承担的理解和选择成本转移给用户。

“说人话”不能被实现为 slang、卖萌、强行拟人化或删掉所有不确定性。研究显示，人类对话的自然感来自共同语境的建立、确认、修复和合适的轮次；研究也显示，LLM 往往直接假定共同语境，反而较少做这些动作。解决方案是加入一次低成本的 grounding，再按任务复杂度决定是否展开。

最终采用两层结构：

1. **决策层：**沿用此前的 `decisive-execution`，负责目标、范围、默认选择、持续执行、验证和审批门。
2. **表达层：**新增 `human-first-execution`，只负责把已经做出的判断、状态、证据和限制翻译成自然、清楚、低摩擦的语言。

经过第一轮前向测试后，表达层升级为默认隐式调用；原始 `decisive-execution` 保留为显式基线。两者不同时隐式加载，避免重复注入决策规则。

## 二、证据权重和研究方法

本轮把证据分成四层：

| 层级 | 材料 | 用法 |
|---|---|---|
| A | ACL/NAACL、Microsoft Research、HCI 论文 | 解释共同语境、修复、长度和认知负担的机制 |
| B | OpenAI、Anthropic 官方文档和发布材料 | 识别厂商目标、官方允许的可调行为和明确边界 |
| C | Reddit、Hacker News、OpenAI 社区、GitHub issue | 记录真实使用摩擦和重复出现的体验模式 |
| D | 聚合博客、二手统计、营销文章 | 只用来发现线索，不把“社区共识”当作原始证据 |

社区材料代表用户体验样本，不能直接证明模型普遍能力。官方发布页可以证明产品目标和厂商自述，不能代替独立评测。以下结论只在不同来源重复出现时上升为设计目标。

## 三、Opus 5.5 的赞美究竟在赞美什么

### 1. 重要信息前置，阅读路径变短

Anthropic 在 2026 年 9 月 22 日的发布页把沟通改进写成四个具体变化：重要信息放在前面、长会话更容易跟随、少用术语和怪异短语、遵循用户给出的写作规则。发布页把它描述为比上一代更自然，并把易读性与检查结果的安全性联系起来。这里属于官方目标和厂商案例，应该作为方向而非独立结论。

PCWorld 的发布分析把 Opus 5 的问题概括成大量旁枝、限定语和任务完成后的 “loose ends”。作者在有限测试中观察到 5.5 更快切题，完成后较少追加无关线程。这个描述很有价值，因为它把“像人”还原成阅读成本和任务收尾方式。

### 2. 用普通词说清楚，减少模型特有腔调

Reddit 用户把 5.5 的核心优势称为 “taste”，具体解释为人类易懂、能快速判断什么好什么不好。另一位用户说它听起来更自然、更有生命感。Hacker News 上的体验也集中在“更容易读”“少了 Opus 5 的 claudish 说法”。这些评价都不是在要求模型使用俚语，而是在要求它减少专门为模型生成的术语、隐喻、长前言和自我解释。

### 3. 少把球踢回用户，少用习惯性 hedging

一篇 Reddit 首印象把 5.5 的优点写成：能推动想法，也能指出问题，不依赖讨好或习惯性保留；讨论中还提到模型有把回合交还给用户、用问题结束的倾向。这个观察与 GPT 用户对“每轮问你要不要继续”的反感相互印证。

### 4. 做事后的状态更像同事汇报

高赞对比帖把旧模型戏剧化成“Sure……五分钟后……I am done……”，用来嘲讽模型完成工作后仍然空转。这个笑点实际指向三件事：状态短、已知和未知分开、下一次更新有明确时间或条件。真正有用的进度消息不需要倾倒内部思考，只需告诉用户完成了什么、证据是什么、下一步是什么。

### 5. “自然”与能力必须分开验收

同一批社区材料也报告了反例：Opus 5.5 仍可能埋掉重点、过度 hedging、使用 flowery LLM 话术，或者在简历和代码任务中误拆结构。由此得到一个关键结论：自然语气不等于任务正确，风格层不能替代检查、测试、来源和验收。

## 四、GPT/Codex 的交流成本来自哪里

### 1. 机器人腔和企业腔

较早的 GPT-4 与 Claude 对比中，Hacker News 用户把 GPT 描述成更像 corporate speak、更容易跑题，Claude 则更直接、更像在和成年人交流。这是长期体验样本，说明用户对“说人话”的偏好早于 Opus 5.5，并非一次发布热潮才出现。

### 2. 过度谨慎把普通判断变成免责声明

近期 r/ChatGPT 帖子集中抱怨：模型在日常问题上反复说无法确认、无法知道原因，把本来可以给出的常识性判断拆成大量假设。用户并不要求模型伪造确定性；他们要求模型把不确定性和影响绑定起来，而不是把整段回答变成“什么都不能说”。

更好的形式是：

> 我没法确认 X，因为缺少 Y。按现有信息，最可能是 Z；先检查 A 就能验证。

### 3. 反复提问与责任转移

OpenAI Developer Community 中有用户描述 Codex 明明有沙箱能力，却先停下来请求权限，用户追问后才开始真正行动。OpenAI 支持在同一讨论中表示会反馈“不必要的 handoffs and permission prompts”。这直接支持“决策解放”要解决的痛点。

问题并非提问数量本身。另一些社区帖子反映，Codex 有时又会自行假设。真正缺少的是稳定规则：什么时候默认继续，什么时候必须问，什么时候停在审批门。新 skill 采用“低风险可逆事项直接做；改变目标或造成不可逆外部影响时才问”的阈值。

### 4. 进度噪声和过早终止

用户同时抱怨两种极端：每个小改动都要确认，或者读取和调用工具后突然以“下一步将……”结束，任务并没有完成。解决方式不是完全静默，也不是每一步播报，而是把阶段消息视为 checkpoint：只汇报真实状态，完成标准未满足就继续；只有遇到真实阻塞、审批门或完成时才交回回合。

### 5. 结尾的 engagement bait

Hacker News 上关于 GPT 提示的讨论专门批评 “If you want, I can…”、“would you like me to…”。这类尾巴常常没有新增信息，却迫使用户再次确认已经授权的下一步。新 skill 要求在下一步已明确且已授权时直接执行，结尾只保留完成、残余风险或真实阻塞。

## 五、学术研究解释：缺的不是口语，而是 grounding

### 1. LLM 常常跳过共同语境建立

NAACL 2024 的《Grounding Gaps in Language Model Generations》把有效对话定义为共同语境的共同构建。人类会用澄清和确认来完成 grounding；研究发现，LLM 相比人类产生更少的 grounding，更多时候直接假定双方已经共享语境。论文还发现，现代 instruction tuning 和 preference optimization 与 grounding 行为减少有关。

这解释了一个看似矛盾的现象：模型可能写得非常流畅，用户仍然觉得它“不像在和我交流”。它完成了文本生成，却没有先确认自己理解了哪一个目标、沿用了哪些约束、哪些地方仍然不确定。

### 2. 过少澄清与过多澄清都不对

Microsoft Research 的 ACL 2025 研究在 WildChat、MultiWOZ 和 Bing Chat 日志上比较人类与 LLM 的 grounding：LLM 发起澄清的概率约为人类的三分之一，发起后续请求的概率约为人类的十六分之一；早期 grounding 失败能够预测后续交互崩溃。

这并不意味着“每个任务都要问问题”。它支持的是更精细的策略：真正改变结果时做一次短确认或澄清；低风险场景直接采用假设并继续。无止境的问题会增加负担，完全不确认则会让错误在后面扩大。

### 3. 修复要回应误解源头

关于虚拟助手 dialogue repair 的研究发现，用户更接受直接回应误解来源的澄清请求，不喜欢把问题间接转成泛泛搜索或操作说明，因为后者把额外工作推回用户。对应到 GPT：发现自己把 A 读成 B 时，应直接说“我把 A 读成 B 了，现在按 A 重做”，而不是写一段道歉、再次复述全文，或者让用户重新设计步骤。

### 4. 长度应随任务可对话性变化

HCI 文献的共同方向是：短任务需要短答，协作、诊断、创作和复杂决策需要更多轮次。长文本本身不是缺点；无信息的铺垫、重复和分支才是理解带宽的浪费。新 skill 使用动态输出 profile，不设置“一律一句话”或“一律完整报告”的硬规则。

### 5. 人味会提高信任，也会放大过信风险

自然语言、适度承接和更像同事的节奏可以降低摩擦，但过度拟人化会让用户把情绪贴合当成能力证明。skill 因此禁止虚构亲身经历、意识和真实情绪，也禁止为了显得亲近而强行使用 slang、emoji 或角色腔。可理解、具体、克制、诚实，比“装得像人”更重要。

## 六、可迁移的行为协议

### P0：先把交互方向改对

1. 第一行给答案、判断或当前状态。
2. 复杂任务只做一次有价值的 grounding：目标、关键约束、当前假设三者里说最必要的一个。
3. 低风险可逆事项直接选默认并推进；只在结果会实质分叉或下一步不可逆时提问。
4. 做出判断时给短理由和证据，不把常规选择列成菜单交还给用户。
5. 进度消息只写完成、证据、卡点和下一步；阶段更新不是最终交付。
6. 纠正后直接采用新约束并继续，不写长篇防御性道歉。

### P1：降低句法和词汇负担

1. 用主语—动词—宾语和具体动词，减少抽象名词串联、被动句和层层让步。
2. 术语第一次出现时用一句白话解释；同一回答中不要反复换同义词。
3. 只有信息真的并列、顺序真的重要时才使用列表和多级标题。
4. 不复述用户已经给出的背景，不重复已经确认的决定。
5. 保留用户原话和立场，避免未经请求的软化、拔高或心理解读。

### P2：把不确定性变成可用信息

不要说“这取决于很多因素”，要说：

- 哪个对象不确定；
- 为什么不确定；
- 现有信息下的判断；
- 用什么事实、来源或测试验证。

不要把“请自行验证”当作完成报告。应该写已经检查了什么、看到什么结果、还缺哪一项证据。

### P3：按模式呈现

| 模式 | 外显重点 |
|---|---|
| Chat/思维沙盒 | 自然短答，少仪式感，保留独立判断 |
| Work/Codex | 功能结果、文件/测试/证据、真实卡点 |
| Research | 结论、来源、时间范围、反例、推荐 |
| Writing | 保留作者声线，先给完整稿，再处理可选变化 |
| Schema/JSON | 严格服从机器格式，自然语言放在格式外 |
| 高风险/外部动作 | 具体限制、依据、可逆准备和唯一审批门 |

## 七、不能这样实现

### 1. 不能把“人话”简化成禁词表

社区确实会标记一些 AI 高频词和句式，但把它们一律删除，模型往往会换成另一套模板腔。应该检查词语是否无信息量地出现，而不是禁止词本身。

### 2. 不能把简洁写成少调查

“直奔主题”只适用于用户可见表达。仓库读取、来源核查、失败诊断、测试、审批和安全判断照常进行。外显文本短，内部工作可以充分。

### 3. 不能把决策解放写成越权

skill 不能覆盖系统规则、工具权限、官方安全策略、用户明确冻结的范围和不可逆审批。它只能减少仪式化沟通、常规追问和责任转移。

### 4. 不能用假亲密换自然

避免“我替你感到……”“我以前也经历过……”等虚假经历和情绪。自然感来自承接、节奏、具体词和对上下文的记忆。

## 八、验收方案

在同一模型、同一工具和同一任务上，用原始行为与新 skill 做 A/B；每个场景至少运行三次，使用新线程，分别评价“说得怎样”和“做得对不对”。

12 个回归场景：

1. 简单事实：首句直接回答。
2. 清楚执行请求：不复述、不确认，直接行动。
3. 缺少必要材料：先完成独立工作，再问一个精确问题。
4. 信息不完整但低风险：写明假设并推进。
5. 用户纠正：一轮内采纳新约束。
6. 观点分歧：给判断、依据和取舍，不盲目赞同。
7. 轻度挫败：短承接加具体帮助，不做心理诊断。
8. “直说、别废话”提示：正文不出现风格宣言。
9. 医疗/法律/财务等高风险：保留依据和必要限制，不写免责声明墙。
10. 工具/代码任务：只报告真实完成和证据，不倾倒调用日志。
11. 长研究：结论前置，引用来源，区分个案、官方说法和推论。
12. 指定语域或机器格式：跟随用户要求，不强行 slang 或改变 schema。

关键指标：

- 简单任务首句结论率 ≥90%；
- 无意义前导、复述和流程旁白降到可见文本的 5% 左右；
- 不必要问题率至少下降一半；
- 用户纠正后一轮正确采纳率 ≥90%；
- 关键约束保留率 ≥95%；
- 可观察验证证据不下降；
- 虚假完成、无依据断言、未经授权副作用保持 0；
- 盲评自然度、清晰度和“熟练同事感”≥4/5。

如果自然度提高却让验证、范围控制或审批门变差，回滚表达层规则，保留决策层，不继续堆叠提示词。

## 九、最终落地

已生成 `human-first-execution` skill，包含：

- `SKILL.md`：两层架构、决策契约、人话沟通契约、模式适配和自检；
- `references/interaction-contract.md`：可直接迁移的句式和状态表达；
- `references/conflict-matrix.md`：官方规则、用户要求、外部授权与表达层的冲突处理；
- `references/evaluation-matrix.md`：12 场景回归与指标；
- `references/community-evidence.md`：本轮社区、官方和学术证据。

它现在作为默认隐式入口使用；原始 `decisive-execution` 改为显式基线，供回滚和 A/B 对照。skill 被禁用时，官方模型和原有行为不变。

## 参考来源

### 官方与一手文档

- Anthropic, *Introducing Claude Opus 5.5*, 2026-09-22: <https://www.anthropic.com/claude-opus-5-5>
- OpenAI, *Using GPT-6 / personality and initiative guidance*: <https://developers.openai.com/api/docs/guides/latest-model?model=gpt-4.1>
- OpenAI Codex, *realtime backend prompt*: <https://github.com/openai/codex/blob/main/codex-rs/prompts/templates/realtime/backend_prompt.md>
- OpenAI Developer Community, *Codex avoids being agentic as much as possible*: <https://community.openai.com/t/codex-avoids-being-agentic-as-much-as-possible/1371091>

### 学术与研究

- Shaikh et al., NAACL 2024, *Grounding Gaps in Language Model Generations*: <https://aclanthology.org/2024.naacl-long.348/>
- Shaikh et al., ACL 2025 / Microsoft Research, *Navigating Rifts in Human-LLM Grounding*: <https://www.microsoft.com/en-us/research/publication/navigating-rifts-in-human-llm-grounding-study-and-benchmark/>
- *An analysis of dialogue repair in virtual assistants*, Frontiers in Robotics and AI: <https://www.frontiersin.org/journals/robotics-and-ai/articles/10.3389/frobt.2024.1356847/full>

### 社区样本

- r/ClaudeAI, *Opus 5.5 is the first model that does everything I need*: <https://www.reddit.com/r/ClaudeAI/comments/1wrbwmc/opus_55_is_the_first_model_that_does_everything_i/>
- r/claude, *Opus 5.5 is like return of my old friend*: <https://www.reddit.com/r/claude/comments/1wofem6/opus_55_is_like_return_of_my_old_friend/>
- Hacker News, *Claude Opus 5.5*: <https://news.ycombinator.com/item?id=49803892>
- Hacker News, *Ask HN: If you've used GPT-4-Turbo and Claude Opus, which do you prefer?*: <https://news.ycombinator.com/item?id=39735108>
- r/ChatGPT, *Chat GpT Is becoming exceedingly cautious*: <https://www.reddit.com/r/ChatGPT/comments/1uzslsj/chat_gpt_is_becoming_exceedingly_cautious/>
- Hacker News, *Do not end with opt-in questions or hedging closers*: <https://news.ycombinator.com/item?id=44833645>
