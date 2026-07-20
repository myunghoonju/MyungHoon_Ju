state: PASS

reason: The title "fix(agents): correct typo in commit-msg-reviewer description" follows the Conventional Commits `type(scope): subject` pattern correctly (valid type "fix", scope "agents" matches the file's location under `.claude/agents/`, imperative lowercase subject, 60 chars, no trailing period). The body accurately reflects `git diff --cached`, which only changes "corectness" to "correctness" in the `description` field of `.claude/agents/commit-msg-reviewer.md`, matching the draft's description of a typo-only, non-behavioral change.
