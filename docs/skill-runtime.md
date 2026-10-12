# Skill runtime prerequisites

The complete selected Skills are committed under `.agents/skills/`. A clone or source archive needs no original workspace, source repository, release cache or fixed machine path for discovery.

Read each selected SKILL.md and its references before execution. Install the interpreter and packages it declares (for example Python requirements.txt or Node package.json); invoke scripts through their documented interpreter. Set up personal credentials using the Skill’s external configuration instructions. Keep .env files, SSH keys, login state, environments, caches and run outputs outside committed Skill payloads.

The project lock records the selected source commit and update baseline. Git tracks local edits. `skill sync` in a managed workspace restores missing tracked files from this project’s HEAD; it never selects a newer pool version. Update only through an explicit Skill update and inspect Git diff before committing.

Verify file installation, actual Agent discovery and a representative script execution separately. Paid calls and external messages require their own task authorization.
