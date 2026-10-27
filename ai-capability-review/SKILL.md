---
name: ai-capability-review
description: Reviews how the user prompts and works with AI chat and AI coding agents, scores them on 15 habits, and gives evidence-based improvements. Use when the user asks to review, audit, score or improve their AI skills, prompting, or how they use Claude, Claude Code or other AI tools.
---

# AI capability review

Give the user an honest, evidence-based review of how they work with AI, and the few changes that would improve their results most. Every score and every recommendation needs a **receipt**: a quote, file or pattern you actually saw. No receipt, no judgment.

This review is read-only. Never change the user's files, and create no output files: the report goes in chat.

## Step 1: Gather receipts

Find the user's prompts yourself. Don't ask the user for anything until you've checked every source below. Read only what tells you how the user works with AI.

### Prompts

Check each source that exists and that you can reach. Aim for 30–50 prompts in total, spread across several projects and the last few weeks rather than one session.

| Source | Where | What counts as a prompt |
| --- | --- | --- |
| Past chats (Claude.ai, Claude app) | Your chat search or recent-chats tool, if you have one. Read 10–20 recent chats, favouring ones where the user asked to build, plan or research something. | The user's own messages |
| Claude Code prompt log | `~/.claude/history.jsonl`, one JSON object per line | The `display` field. `project` says which folder it came from. |
| Claude Code transcripts | `~/.claude/projects/<folder>/<session>.jsonl` | Lines with `"type": "user"` whose `message.content` is a string, or a list holding `text` blocks rather than `tool_result` blocks. Skip lines with `isMeta` or `isSidechain` set to true. |
| Codex CLI | `~/.codex/history.jsonl` | The `text` field |
| Cursor | `~/Library/Application Support/Cursor/User/globalStorage/state.vscdb` on macOS (`%APPDATA%\Cursor\User\...` on Windows, `~/.config/Cursor/User/...` on Linux), a SQLite database. Open it read-only. | In the `cursorDiskKV` table, rows whose key starts with `bubbleId:` and whose JSON has `"type": 1`. The prompt is the `text` field. |

Start with the prompt logs: they hold only what the user typed, so they're the fastest. Use transcripts for the conversation around a prompt, for example to see how the user gave feedback after the AI's first attempt (habit 9).

Whatever the source, score only what the user typed. These don't count: assistant and system messages, tool output, slash commands on their own (like `/clear`), and messages the tool added automatically, which start with an XML-style tag such as `<command-name>`, `<task-notification>` or `<system-reminder>`. Text the user pasted counts as context they supplied, not as wording they wrote.

Read only the prompt fields listed above. Never open credential or auth files in these folders, such as `oauth_creds.json`, `.credentials.json`, `auth.json` or `.env`.

### Project setup

If you're in a project folder, also read `CLAUDE.md` or `AGENTS.md`, anything in `docs/` (product brief, PRD, roadmap, design or brand files), `.claude/settings.json` (check for hooks), skills folders, tests, CI config, and the last 30 commit messages.

### Privacy

Before quoting anything as a receipt, redact credentials, API keys, tokens and personal data (names, emails, phone numbers, addresses), for example `sk-…[redacted]`. Keep enough of the quote to show the habit.

### If you're short of prompts

Ask the user only after you've checked every source. If a source exists but you couldn't read it (a permission prompt was refused, a tool was missing), name it and ask whether you may read it. Only if you still have fewer than 5 real prompts, ask the user to paste enough recent prompts to bring the total to 5, plus a sentence on how they usually work. Wait for their reply, then count again before scoring.

**Done when:** you can list each source you checked and roughly how many prompts or files it gave you, and you have at least 5 real prompts.

## Step 2: Score the 15 habits

Score every habit 0 (not yet), 1 (sometimes) or 2 (consistently), each with a one-line receipt. If you have no receipt either way, mark it "no evidence" and score it 0. Never guess upward.

**Foundations**

1. **Full context:** explains who it's for, why it exists, how it'll be used, and what they don't know yet, rather than one-line asks.
2. **Interview first:** asks the AI to question them before it plans or builds.
3. **Invites pushback:** asks for research and honest critique, not agreement.
4. **Thinking before building:** works out the what and why first (chat, research), then has the AI write the brief for the coding agent.
5. **Docs before code:** the project has written intent (product brief, roadmap, design rules) that the agent reads instead of guessing.
6. **Small, checkable steps:** work is split into tasks that each say how to check they're done, and each phase leaves something working.
7. **Fights overcomplication:** standing rules like "simplest solution first" and "only change what's needed", and cuts back when the AI overbuilds.
8. **Taste as instructions:** specific fonts, colours, references and named things to avoid, not "make it look modern".
9. **Specific feedback:** says exactly what's wrong and why, not "make it better", and iterates on prototypes before building.
10. **Reuse:** prompts and workflows they repeat are saved as skills, templates or commands.

**Top 1%**

11. **Finish line first:** prompts open with the outcome and what "done" means, before the background.
12. **Lean context:** always-loaded instructions are short, and detailed docs are split up and read only when needed.
13. **Enforced, not requested:** important rules are checked automatically (hooks, tests, CI), not just written as instructions the AI might forget.
14. **Outcomes, not just tasks:** sometimes hands over a goal with a measurable bar and lets the agent work toward it on its own.
15. **Tested prompts:** keeps a few test cases for important prompts or skills and re-runs them after changes.

**Done when:** all 15 habits have a score and either a receipt or "no evidence".

## Step 3: Write the report

Write the report in chat, using this structure, in this order:

1. **Summary.** Two or three sentences on how they use AI today, their total out of 30, and their level: 0–10 Starter, 11–20 Builder, 21–26 Pro, 27–30 Top 1%.
2. **Scorecard.** A table: habit, score, receipt.
3. **Keep doing.** Their three strongest habits, with the receipt for each.
4. **Top 3 improvements.** The three changes that would improve their results most. These aren't always the three lowest scores; weigh what they're trying to do. For each:
   - What you saw (the receipt)
   - Why it matters for the results they get
   - One change to make this week
   - A before/after: rewrite one of their real prompts, or one section of their real files, to show the change
5. **Copy-paste starters.** For anything fixable in a file (a `CLAUDE.md` rule, a prompt template, a hook), give the exact text to add and where it goes.
6. **Do this first.** The single most important next step, in one sentence.

Write in plain English, and explain any technical term (like "hook") in a few words the first time. Be direct: if a habit is costing them results, say so. Keep the whole report readable in about five minutes.

**Done when:** every section is present, each improvement has a before/after built from the user's own material, and every claim traces to a receipt.
