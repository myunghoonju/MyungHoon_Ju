---
title: "Claude Code Diary"
date: "2026-03-07"
---

#### Claude Code Diary

#### Harness
 - [practice-01](https://github.com/myunghoonju/MyungHoon_Ju/tree/main/harness/practice-01)

---

### 2026-03-06

**한 일**
- Pro 구독 결제
- iterm에서 아래 명령어로 네이티브 설치
```bash
curl -fsSL https://claude.ai/install.sh | bash -s stable
```

### 2026-03-10

**한 일**
- 내부 명령어들을 직접 실행하며 익힘
```text
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

### 2026-03-15

**한 일**
- 오픈소스 기여 시도
  - 기여 대상: armeria
  - Claude Code로 가장 쉬운 기여 주제를 탐색 후 [PR 제안](https://github.com/line/armeria/pull/6665)

### 2026-03-17

**배운 점**
- CLAUDE.md와 `@{파일명}.md` 형식의 파일 생성
- `@` 기호로 표시해두면, CLAUDE.md를 읽을 때 해당 파일명이 있으면 에이전트가 함께 읽음

### 2026-03-19

**배운 점**
- CLAUDE.md는 프로젝트별 가이드라인, 선호사항, 지시사항을 담음
- `/init`으로 CLAUDE.md 파일 생성
  - 프로젝트 가이드로 구체화해서 사용
- 스코프 2가지
  - user (`.claude/CLAUDE.md`)
  - project (`{proj}/CLAUDE.md`)

### 2026-03-22

**배운 점**
- 토큰
  - 한국어가 영어보다 대략 3배 더 소모됨

### 2026-03-28

**배운 점**
- Claude Code 툴 목록 정리
```text
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
