# 开源去 AI 味项目研究

调研日期：2026-10-12。范围：中文文案终稿审核可借鉴的公开仓库与 Agent Skills。通过 GitHub API 读取当前源码、README 与许可证；未安装或执行候选代码，未调用模型、检测器或付费接口。下列链接指向动态分支，后续使用时应核对当时内容。

## 结论

建议以 `op7418/Humanizer-zh` 的中文编辑约束为基础，借鉴 `blader/humanizer` 对结构性套路的识别，以及 `Hyacehila/humanizer-zh-next` 的商务文案条件保护；最后形成一次“定位问题 → 局部修改 → 核对事实和语气”的终稿审核。

目前证据支持的是“编辑中应重点检查的表达模式”，不是中文词频排行榜，也不能从单词命中推断作者是不是 AI。最值得优先处理的是不增加信息的假对比、铺垫、拔高和重复收尾，而不是机械替换所有正式词汇。

## 六个代表性候选

| 项目 | 本次核实的许可 | 内容与适配程度 | 适合借鉴 | 不宜直接照搬 |
| --- | --- | --- | --- | --- |
| [blader/humanizer](https://github.com/blader/humanizer) | [MIT 正文](https://github.com/blader/humanizer/blob/main/LICENSE)，版权 Siqi Chen | 英文 Skill；本次主文件标记 3.1.0。高相关 | 模式先标记、再改写、对照检查；结构问题优先；作者样本可覆盖通用风格 | 当前默认禁长破折号；把某些词写成无论出现在哪都算信号，中文不能照搬 |
| [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) | [MIT 正文](https://github.com/op7418/Humanizer-zh/blob/main/LICENSE)，版权 歸藏 | 中文 Skill；主文件修订标记 2026-09-23，共 31 条。最适合基础层 | 不新增事实、不丢独立信息；保留条件、否定、时间、归因、强度；有“应保留”反例 | 条目标题中的“AI 高频词”没有给中文频次、样本量和基准，不可当统计结论 |
| [Hyacehila/humanizer-zh-next](https://github.com/Hyacehila/humanizer-zh-next) | [MIT 正文](https://github.com/Hyacehila/humanizer-zh-next/blob/main/LICENSE)，版权 contributors | 中文 Skill；主文件 2.0.0，另有商务、学术、基金分支。高相关 | 按文体审核、审阅不默认写回；商务分支核对卖点、来源、行动入口与真实限制 | 主文件较长，项目应提炼终审所需内容，不要默认加载所有文体规则 |
| [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) | [MIT 正文](https://github.com/hardikpandya/stop-slop/blob/main/LICENSE)，版权 Hardik Pandya | 英文精简 Skill。可作反模式参考 | 空铺垫、假对比、戏剧化碎片、空洞金句、节奏重复等检查 | “删除所有副词”“禁止被动句”“两项优于三项”“每句需要人作主语”过于绝对；35/50 分阈值不是验证过的指标 |
| [obra/the-elements-of-style](https://github.com/obra/the-elements-of-style) | README 与 package.json 声明 Public Domain；根目录本次未发现 LICENSE。README 的公有领域说明明确涉及 1918 年 Strunk 文本 | 实际包含 `writing-clearly-and-concisely` Skill；通用英文编辑。中高相关 | 具体语言、删除赘词、主动作句、相关词靠近；可放在成稿后的编辑环节 | 不应将正文公有领域说明自动外推到一切新增包装文件、所有地区；英文语法规则不直接适用于中文 |
| [lynote-ai/humanize-text](https://github.com/lynote-ai/humanize-text) | [MIT 正文](https://github.com/lynote-ai/humanize-text/blob/main/LICENSE)，版权 Lynote.ai | 有 Python 多轮改写/翻译链与结构改写训练数据流水线；公开代码与商业服务并存。低适配当前轻量终审 | 关注语义漂移、过度改写、结构损坏等失败类型 | 旧翻译链最终回英语、外部服务多、容易漂移；检测器驱动目标不同；商业模型非本仓开源交付，营销效果数字不能作为独立证据 |

六项的许可证均查阅了项目自身文本或声明，不以“GitHub 能打开”代替开源许可。MIT 项目如复制或实质改编其材料，应保留适用版权与许可文字；只记录自行分析和链接则没有必要把整套上游搬进项目。

额外观察到 [ai-zixun/humanizer-zh](https://github.com/ai-zixun/humanizer-zh) 也是 MIT，强调中文翻译腔、文章主线和文体，但含作者声音扩展、默认禁破折号和特定术语替换；本项目不需要增加作者模仿流程，故不列为首选。

## 源码核实要点

### humanizer：当前版本已把结构放在词汇前

[SKILL.md](https://github.com/blader/humanizer/blob/main/SKILL.md) 的顺序为：假对比、戏剧化单句收尾、伪深度、宣布进入正文、回应不存在的反对意见；然后才到强凑三项、重复起句、破折号、限定词堆叠与词汇。

这支持“先审句子提供了什么信息，再查词”的设计。该 Skill 说词汇习惯会随模型版本变化；这属于维护者编辑判断，并非对中文模型的统计测量。其英文词表包括 `delve`、`pivotal`、`tapestry`、`testament`、`underscore`、`showcase`、`landscape` 等；项目不能把英文词表逐个翻译成中文后宣称得到中文高频榜。

### Humanizer-zh：31 条不等于 31 个禁令

[SKILL.md](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md) 明确说单个词、标点、三项列表或四字词不是修改理由，也不证明文本来自 AI。其正反例特别适合作为本项目的审核样例：

- “这不仅是一个导出按钮，更是通往高效工作的全新入口。它可以导出 CSV。”去掉虚张声势，保留功能。
- “错误发生在保存阶段，而不是上传阶段。”需要保留真实对比。
- “控制器使用闭环反馈调整输出。”需要保留技术术语。
- “只有在缓存开启时可能有效，结果尚未验证。”需要保留条件与不确定性。

这些是上游教学例子，不是来自真实用户语料的频次证据。

### humanizer-zh-next：商务文案的事实与行动条件

[商务与营销编辑](https://github.com/Hyacehila/humanizer-zh-next/blob/main/references/commercial-editing.md) 检查清晰度、声音、读者利益、证据、具体性、情绪、行动条件，但不要求每篇短文走七轮。

对本项目尤其重要的是保留费用、资格、有效期、按钮和入口、承诺边界；不能为了文案具体而补造收益数字、免费试用或处理时限。来源归因必须保留：“供应商声称减少 30%”不能改成“减少 30%”的已验证事实。

### stop-slop：可借鉴问题定义，不采用绝对禁令

[SKILL.md](https://github.com/hardikpandya/stop-slop/blob/main/SKILL.md) 的表达检查短小直接。但其所有副词、被动句都删除的要求会改变语义，固定打破三项结构也可能丢失真实信息。本项目应该将这些词和结构设为需要结合上下文的线索，而不是通过条件。

### writing-clearly-and-concisely：确有实际 Skill 路径

[SKILL.md](https://github.com/obra/the-elements-of-style/blob/main/skills/writing-clearly-and-concisely/SKILL.md) 引用 Strunk 1918 年写作原则。它有先写草稿、再交给编辑审核的用法，符合本项目“生成末尾一轮”的位置设计。

许可证据分别见 [README](https://github.com/obra/the-elements-of-style/blob/main/README.md) 与 [package.json](https://github.com/obra/the-elements-of-style/blob/main/package.json)。本次不将其表述为已核实 MIT 的仓库。

### humanize-text：不能把商业宣传与开源实现混为一谈

[README](https://github.com/lynote-ai/humanize-text/blob/main/README.md) 公开了旧版中 → 日 → 芬兰语 → 英语链条，以及当前 SFT/KTO 数据构建思路；明确没有交付模型权重、托管端点或当前训练方法的性能承诺。文档同时有自家商业服务推广和自报样例指标。

源码开放不代表生产模型开放，自报“检测通过”也不代表中文文案质量提升。其局限章节承认翻译链会损失精度、术语和引用可能漂移，因此不适合作为本项目第一版方案。

## 中文优先检查清单：有出处的候选，非频率排名

下表按“最容易增加空泛感、且在当前业务文案中值得先审”的编辑优先级组织；不是根据模型样本统计出的概率或排名。

| 类别 | 候选词句 | 问题成立条件 | 保留边界 | 来源 |
| --- | --- | --- | --- | --- |
| 空泛功能和黑话 | 赋能、生态、闭环、抓手、底层逻辑、价值沉淀、全链路、颗粒度、范式、跃迁 | 扎堆却没有说明对象、动作、机制、范围 | 工程闭环、真实统计粒度、既定业务术语 | [next §抽象词和黑话](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 空头赞美 | 卓越、极致、领先、全方位、革命性、沉浸式、护航、无缝 | 没有已知特征支撑，只提高语气 | 真实产品类型、已有品牌定位、被引用的评价 | [next §宣传和广告式语言](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md)、[zh §12](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md) |
| 自动拔高 | 至关重要、具有里程碑意义、开启新篇章、标志着新时代、留下深远影响、彰显了……重大价值 | 普通信息之后补一层没有新信息的意义判断 | 有证据的首次、明确影响、作者真实立场 | [zh §13、15](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[next](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 宣布正文开始 | 让我们深入探讨、接下来让我们看看、下面我们来拆解、以下是你需要知道的 | 仅预告后文，删掉后信息无损 | 必要目录导览、教学步骤提示 | [zh §4](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[next](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 伪深度 | 真正的问题是、归根结底、本质上、底层逻辑 | 后面只是普通观点的重复或无依据定性 | 确实在定义本质、纠正误解或归纳证据 | [next §格言与伪深度](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 假对比 | 不是 X，而是 Y；不仅是 X，更是 Y | 否定的 X 无人提出，Y 只是拔高 | 对比两种真实事实、纠正真实误解 | [zh §1](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[humanizer §1](https://github.com/blader/humanizer/blob/main/SKILL.md) |
| 空泛背景/收尾 | 随着……不断发展、机遇与挑战并存、未来值得期待、让我们拭目以待 | 与具体任务无关，没有独立信息 | 实际增长趋势、真实计划、作者情感、必要总结 | [zh §30、31](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[next](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 无出处权威 | 专家认为、业内普遍认为、相关人士指出、行业报告显示 | 来源不可追溯，却用来撑确定结论 | 原文已有归因要保留；标注缺口，不编机构/引用 | [zh §17](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[next](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |
| 冗余而非强信号 | 值得注意的是、进行分析、进行调整、从某种意义上说 | 增加长度却无作用，或高密度重复 | 正式文体、真实操作状态、必要程度限定 | [zh §27](https://github.com/op7418/Humanizer-zh/blob/main/SKILL.md)、[next](https://github.com/Hyacehila/humanizer-zh-next/blob/main/SKILL.md) |

“首先、其次、最后”“与此同时”“然而”“综上”不列为自动删除词。它们可能表达顺序、同时性、转折或总结；误删会改变意思。三个条目、四字格、破折号、短句也不能单独作为 AI 味结论。

## 后续终审设计建议

这部分是本项目建议，不是候选仓库已经验证的性能。

1. 输入成稿、读者/渠道、必须保留的信息；作者样本可选。没有样本时保留原稿语域，不强迫口语化。
2. 通读结构，定位具体问题：原句、上下文、为什么显得空泛/模板化、是否实际妨碍理解。词表仅帮助发现候选。
3. 对确实存在的问题做最小改写，必要时重写所在句段；没有问题允许原样通过。
4. 对照原稿检查：数字、人名、产品名、链接、活动期限、资格、奖励、条件、否定、归因、确定程度、行动入口是否一致。
5. 交付终稿；需要审阅解释时另附少量问题与改动。不输出“AI 概率”，不用“删词数量”或无依据的自评分代替质量验收。

建议首先积累一小组项目自己的真实文案及人工认可版本，同时保留“命中了却应保留”的反例，再校准哪些规则确实改善本项目文案。在此之前，把词表称为“观察清单/候选表达”，不要称“中文 AI 高频榜”。
