---
name: commit-message
description: "based on staged diffs generate a team of 2 agents Conventional Commits formatted message. when user type 'commit it' this skill is activated"
allowed-tools: Bash, Read, Write
---

# Commit message skill
team of 2 activated sequentially. write commit message with Conventional Commits format


## Workflow
 1. check precondition
    run `git diff --cached --quiet`
    pass when returned exit code 1 otherwise print "stage diff first!" then end.
 
 2. call author
    call `commit-msg-author` agent as a agent tool
    output will be `commit-draft.md` at `_workspace/`

 3. call reviewer
    call `commit-msg-reviewer` agent as a agent tool
    output will be `review-report.md` at `_workspace/`

 4. decision of PASS or REDO
    - PASS: present `_workspace/commit-draft.md` to user and end.
    - REDO: re call author maximum twice with handing reviewer's comment over 

 5. end loop
    condition: PASS or recalled twice
    if maximum called then warn "manual review required" message with returning  the last draft.md file


