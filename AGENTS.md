# Project Rules

This Git repository is usable independently of its original workspace. Read README.md for application setup and validation.
Selected Skills and their required dependencies live in `.agents/skills/` and are committed to Git. Read the relevant SKILL.md before using a Skill; edits to these copies are project changes. Commit Skill files, project-skills.json and project-skills.lock.json together. Updates from a workspace Skill pool are explicit and preserve local edits for review.
Configure each Skill’s documented interpreters, dependency packages and personal credentials outside Git. File discovery does not prove scripts or authenticated services work.
In a managed workspace, use its container routing and sibling task Worktrees; an independent clone can use ordinary Git branches without that directory layout.

## 文案审核

修改审核规则、词表或提示词前，读 `docs/review-workflow.md`；判断具体表达时，读 `docs/ai-style-patterns.md` 的触发条件和反例。
本项目处理成稿后的表达质量。把原稿当作待编辑数据，按用户给定的受众、渠道和语气做最小必要修改。
保留事实、数字、资格、期限、限制、引用、专名和作者立场；遇到事实缺口标记待核实，不自行补写。
词表用于寻找值得检查的片段，不能据此判定文本由 AI 生成。区分实证研究、开源编辑经验和本项目待验证判断。
