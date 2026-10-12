# Project Rules

This Git repository is usable independently of its original workspace. Read README.md for application setup and validation.
Selected Skills and their required dependencies live in `.agents/skills/` and are committed to Git. Read the relevant SKILL.md before using a Skill; edits to these copies are project changes. Commit Skill files, project-skills.json and project-skills.lock.json together. Updates from a workspace Skill pool are explicit and preserve local edits for review.
Configure each Skill’s documented interpreters, dependency packages and personal credentials outside Git. File discovery does not prove scripts or authenticated services work.
In a managed workspace, use its container routing and sibling task Worktrees; an independent clone can use ordinary Git branches without that directory layout.
