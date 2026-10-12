# Project Rules

This Git repository is usable independently of its original workspace. Read README.md for application setup and validation.
Selected Skills and their required dependencies live in `.agents/skills/` and are committed to Git. Read the relevant SKILL.md before using a Skill; edits to these copies are project changes. Commit Skill files, project-skills.json and project-skills.lock.json together. Updates from a workspace Skill pool are explicit and preserve local edits for review.
Configure each Skill’s documented interpreters, dependency packages and personal credentials outside Git. File discovery does not prove scripts or authenticated services work.
In a managed workspace, use its container routing and sibling task Worktrees; an independent clone can use ordinary Git branches without that directory layout.

## 文案审核

本项目独立设计，规则来源为用户指出的 AI 味反例及其反馈，以及维护者确认吸纳的社区案例。不引入其他仓库、Skills 或通用写作词表的判断逻辑。
执行审核或维护规则前，读 `docs/review-workflow.md` 和 `rules/negative-checklist.md`。规则库是禁止模式的唯一维护源。
用户说某句话 AI 味重时，直接记录原句、日期和反馈，提炼成可反向检查的表达模式，补充同义变体、处理动作和自拟改写示例；重复模式合并到原条目，新增模式使用稳定编号。
按规则库逐条反向检查成稿。只修改命中的表达，保留原意与具体事实；默认交付终稿，按用户要求再展示命中项。
本项目的答复、审核说明和改写结果也执行这套检查。
