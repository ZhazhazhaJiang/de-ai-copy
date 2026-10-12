# 去除 AI 味

在文案初稿完成后，增加一轮编辑审核，减少空泛、模板化和不合语境的表达，同时保留原意、事实和作者语气。首阶段以中文文案为主。

## 当前交付

- [开源仓库与 Skills 调研](docs/open-source-research.md)：来源、许可、可借鉴点和使用边界。
- [AI 味词汇与句式分析](docs/ai-style-patterns.md)：审核优先级、触发条件、反例及证据边界。
- [单轮终审流程](docs/review-workflow.md)：输入、审核顺序、输出和完成条件。
- [可复制的审核提示词](prompts/final-review.md)：可随成稿一起交给模型进行人工试用。
- [编辑示例](examples/review-cases.md)：需要修改、应当保留和信息不足三类情况。

当前完成的是项目初始化、调研及审核设计；尚未开发自动审核程序、安装第三方 Skill 或开展真实文案效果评测。

## 使用方式

将审核提示词与原稿一起提供，并尽量注明渠道、受众、目标、语气及必须保留的信息。一次审核输出问题片段和修改后全文；事实缺口单独列出。没有明确问题时原样返回，不为完成审核而改写。

研究资料不支持“中文 AI 味词汇频率排行榜”。本项目维护的是有上下文条件的编辑规则，不输出 AI 生成概率，也不以通过检测器为目标。

## 后续实现

先用真实文案校准规则，再将审核提示词封装为写作流程的最后一个步骤。词表只负责提示候选问题，语义审核负责判断及最小改写，最后在同一轮中核对事实保留情况。暂不绑定技术栈或模型供应商。

## 本地检查

本阶段没有应用依赖或运行命令。在 `main/` 中可检查文档补丁：

```powershell
git diff --check
```

管理工作区中可使用现有工具同步空 Skill 配置并检查工作区：

```powershell
python ../../../../../ops/workspace-management/workspace.py skill sync --space ../../../../.. --project .
python ../../../../../ops/workspace-management/workspace.py doctor --space ../../../../..
```

项目采用空 Skill 配置；[Skill 运行说明](docs/skill-runtime.md)仅在后续明确引入依赖时适用。

2026-10-12 初始化检查：文档本地链接与编码检查通过，空 Skill 配置连续同步两次均无变更。工作区级 `doctor` 在检查管理工具自身时返回 `Installed management snapshot has drifted`，尚未完成全工作区检查；该问题在本项目范围之外，未修改管理工具快照。
