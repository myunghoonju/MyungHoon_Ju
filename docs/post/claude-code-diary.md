#### Claude Code Diary

> 2026-03-06
```text
- paid pro subscription  
- native install via iterm on following command
    curl -fsSL https://claude.ai/install.sh | bash -s stable    
```
> 2026-03-10  
```text
- running internal commands
  help
  clear
  exit
  model
  login & logout
  permissions
  status
  context
  doctor
  release-notes  
```
> 2026-03-15  
```text
- Trying out opensource contribution  
   - where to contribute
       - armeria
   - what did i do
      - search the easiest subject to contribute with claude code
      - make a suggestion(https://github.com/line/armeria/pull/6665)  
```

> 2026-03-17
```text
- create CLAUDE.md and a file named with @{file name}.md 
- with @ symbol claude agent can read it when reading CLAUDE.md if the name found in it.
```

> 2026-03-19
```text
- CLAUDE.md contains project-specific guidelines, preferences, and instructions  
- use /init to create CLADE.md file
    - elaborate with it for a project guide
- 2 scope  
    - user(.claude/CLAUDE.md)
    - project({proj}/CLAUDE.md)

- a good prompt should have
  - rich context  
  - specific goals  
  - expected results

- manage tokens  
  - korean spend it more than english like three times  

```

> 2026-03-28
```text
Claude code tools  

File Operations
  - Read — read files
  - Write — create/overwrite files
  - Edit — make targeted edits to files
  - Glob — find files by pattern
  - Grep — search file contents

  Execution
  - Bash — run shell commands

  Agents
  - Agent — launch specialized subagents (general-purpose, Explore, Plan, etc.)

  Task Management
  - TaskCreate, TaskGet, TaskList, TaskOutput, TaskStop, TaskUpdate

  Planning
  - EnterPlanMode, ExitPlanMode
  - EnterWorktree, ExitWorktree

  Scheduling
  - CronCreate, CronDelete, CronList

  Web
  - WebFetch, WebSearch

  Other
  - AskUserQuestion — ask the user a clarifying question
  - Skill — invoke named skills (e.g. /commit, /update-config)
  - ToolSearch — fetch schemas for deferred tools
  - NotebookEdit — edit Jupyter notebooks
```