---
name: ai-capability-review
description: Reviews how the user prompts and works with AI chat and AI coding agents, scores them on 15 habits, and gives evidence-based improvements. Use when the user asks to review, audit, score or improve their AI skills, prompting, or how they use Claude, Claude Code or other AI tools.
---

# AI capability review

Give the user an honest, evidence-based review of how they work with AI, and the few changes that would improve their results most. Every score and every recommendation needs a **receipt**: a quote, file or pattern you actually saw. No receipt, no judgment.

This review is read-only. Never change the user's files.

## Step 1: Gather receipts

Look at everything you can reach, and skip what you can't:

- **Past chats**, if you can search them. Read 10–20 recent ones, favouring chats where the user asked you to build, plan or research something.
- **Claude Code prompt history**, if `~/.claude/history.jsonl` exists. Sample the user's last 30–50 prompts from it. Use only the text the user typed.
- **The current project folder**, if you're in one: `CLAUDE.md` or `AGENTS.md`, anything in `docs/` (product brief, PRD, roadmap, design or brand files), `.claude/settings.json` (check for hooks), skills folders, tests, CI config, and the last 30 commit messages.

If you found fewer than 5 real prompts, stop and ask the user to paste 3–5 prompts they've recently given an AI, plus a sentence on how they usually work. Wait for their reply before scoring.

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

Use this structure, in this order:

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
