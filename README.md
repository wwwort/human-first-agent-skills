# Human-first execution skills

让 GPT/Codex 少一点模型腔，多一点同事感：先把事情推进到可验证结果，再用普通话把结果说清楚。

这个包包含两个可以公开复核的 Skill：

- [`decisive-execution`](skills/decisive-execution/SKILL.md)：检查现状、承担普通可逆决定、执行、验证，在发布、删除、支付、权限变更等外部效果前停在授权门。
- [`human-first-execution`](skills/human-first-execution/SKILL.md)：保留上述决策和验证契约，再增加结论前置、少复述、低成本建立共同语境、直接承接纠正和更自然的表达。

`human-first-execution` 是组合升级版。通常显式调用它即可；`decisive-execution` 作为旧行为基线保留，方便 A/B 对比、回滚和单独测试。

## 调研得到的痛点

社区对“更像在说人话”的赞美，最后可以落成四个工程行为：重要信息先说、用普通词、删掉无关分支和任务尾巴、普通决定由模型承担。对应的 GPT/Codex 交流摩擦主要是：

- 复述和模板化前言增加解码成本；
- 低风险的文件名、目录和测试选择被退回给用户；
- “下一步我可以……”取代实际推进；
- 模型误解后用客套话绕开纠正源头；
- 为了显得果断而跳过证据，或为了显得谨慎而连可逆动作都不做。

目标不是让模型假装成人，也不是删掉所有谨慎。目标是降低沟通成本，同时保留事实、测试、权限和审批边界。

## 交互式对比

打开 [`demo/index.html`](demo/index.html)，切换模式和场景，查看典型回答前后的差异。页面里的 1–5 分是解释协议的目标 rubric，不是模型基准或用户调研统计。

## 三分钟视频素材

- [`three-minute-script.md`](video/three-minute-script.md)：前 2 分钟讲问题和需求，后 1 分钟讲解决方案和仓库；
- [`subtitles.srt`](video/subtitles.srt)：字幕；
- [`bilibili-description.md`](video/bilibili-description.md)：标题、简介、时间轴和标签；
- [`recording-checklist.md`](video/recording-checklist.md)：录制与发布检查。

## 使用

```text
$human-first-execution

把这个任务推进到可验证完成。普通可逆决策你直接选择，只有真正影响范围、权限或不可逆结果的事项再问我。
```

只需要决策层时：

```text
$decisive-execution

先检查现状，选择低后悔的默认路径，完成一个可验证的工作切片。外部不可逆动作停在审批前。
```

## 证据边界

`human-first-execution` 来自 Temp 包 `human-first-execution-local-bundle.zip`，本次已原样落地到 `D:\asset-hub\payload\skills\human-first-execution`，包含 `SKILL.md`、`agents/openai.yaml`、图标和四份参考文档。`decisive-execution` 来自 `D:\asset-hub\payload\skills\decisive-execution`，参考矩阵也随包复制。

调研材料综合了官方材料、社区体验和人机对话研究，用于提出可观察的交互目标，不是对任何模型的独立性能证明。发布前请补充原始链接、署名和许可证选择。

## 发布前最后一步

本地包、对比页、脚本和字幕已经准备好。GitHub owner/repository URL、许可证和 B 站账号状态仍需由发布者确认；推送和上传属于外部发布动作，完成前请回读公开页面。
