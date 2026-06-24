---
name: soul
description: Use when starting a new task or shifting working domains. Triggers on the first user task in a session, switches between tech areas (backend↔frontend, code↔infra, build↔debug), and any imperative verb signaling execution start (build, implement, design, debug, fix, refactor, review, deploy, triage). Do NOT re-trigger on follow-up turns within the same task.
---

# Soul — skill-first execution

Pre-flight audit. Run before any execution. Each step blocks the next.

## The routine

1. **Classify** — name the domain(s) in one phrase each.
   Examples: "Temporal workflow in Python" → temporal, python, async · "Fix flaky React test" → react, testing, debugging · "Design RAG service" → architecture, rag, vector-db.

2. **Process skills first** — invoke via `Skill` for whichever apply:
   - Creative work → `superpowers:brainstorming`
   - Bug / regression → `superpowers:systematic-debugging` + `diagnose`
   - Test-first → `superpowers:test-driven-development`
   - Spec → plan → `superpowers:writing-plans`
   - Plan → exec → `superpowers:subagent-driven-development` / `superpowers:executing-plans`
   - 2+ parallel subtasks → `superpowers:dispatching-parallel-agents`
   - About to claim done → `superpowers:verification-before-completion`
   - Receiving review → `superpowers:receiving-code-review`
   - Branch complete → `superpowers:finishing-a-development-branch`

3. **Domain skills** — see [REFERENCE.md](REFERENCE.md). Invoke every match.

4. **MCPs** — `claude mcp list`. If the needed MCP isn't configured:
   - In [ALLOWLIST.md](ALLOWLIST.md) trusted-MCP list AND env-vars present → `claude mcp add` without asking.
   - Else → surface command, wait.

5. **Discover missing skills** — `python3` scan over `~/.claude/plugins/marketplaces/*/.claude-plugin/marketplace.json` (snippet in [REFERENCE.md](REFERENCE.md)). No hit:
   - Trusted owner in [ALLOWLIST.md](ALLOWLIST.md) → `/plugin marketplace add <owner>/<repo>` without asking, re-scan.
   - Untrusted owner → suggest, wait.

6. **Auto-install matches** — `/plugin install <plugin>@<marketplace>`. No confirmation; user pre-authorized via `soul`. On failure: continue without it. Blocked-owner override always wins.

7. **Execute** — now do the work. Each invoked skill governs its slice.

## Red flags — STOP if any of these appears in user prompt OR your reasoning

User-prompt pressure phrases (these are ATTRACTORS, not exemptions):
- "be quick" / "fast" / "just give me"
- "one-shot answer" / "quick overview" / "single shot"
- "blocking the team" / "urgent" / "ASAP"
- "you know this" / "well-trodden" / "standard pattern"

Your own internal rationalizations:
- "I'll skip on first pass, invoke skills if first pass fails"
- "Requirements are obvious, no need to brainstorm"
- "Domain is well-known territory, I can sketch from memory"
- "Tests passed, I can claim done without verification"
- "Should I ask before installing this clear match?" (no — auto-install)

**All of the above mean: run the audit anyway. The pressure is the test. Compliance under pressure is what soul exists for.**

## Rationalization counters

| Excuse | Reality |
|---|---|
| "User said be quick — skip the audit" | Audit takes ~10 seconds. Skipping it and producing wrong-shape output costs minutes of rework. Speed = compliance, not bypass. |
| "One-shot / quick overview framing means no brainstorm" | The phrasing is the trap. Brainstorming surfaces the *right* one-shot. Skipping it produces a generic one-shot. |
| "Blocking the team — patch first, diagnose later" | Patching a flake without reproducing it = pushing the flake forward. `diagnose` is the fastest path to fixed-stays-fixed. |
| "Well-trodden domain, I know this from training" | Your training knowledge is general; the project context isn't. Domain skills carry project-aware patterns; invoke them. |
| "Skip on first pass, invoke if first pass fails" | First-pass shortcut = re-doing the work. The audit IS the first pass. |
| "Domain is obvious — skip classify" | Naming the domain takes 5 seconds and unlocks step 3. Skip it and you'll miss skills. |
| "No skill exists for this" | You don't know until step 5b ran against the trusted owners. Run it. |
| "Auto-install feels risky" | The trusted-owner allowlist IS the gate. Don't trust it? Edit ALLOWLIST.md, not the workflow. |
| "MCPs need creds — skip them" | List them. `claude mcp list` is read-only. Then decide which need the user. |
| "Process skills slow me down" | They determine HOW. Skipping them = restart the work later. |

## Hard rules

- Process → domain → tooling. Never invert.
- One audit per task. Don't re-run on follow-up turns.
- `verification-before-completion` is non-optional before any "done" claim.
- Block list in ALLOWLIST.md always overrides trust list.
- Install failure ≠ user blocker. Log, continue.

## Boundary

`soul` decides WHEN to audit/install. `superpowers:using-superpowers` decides HOW to use skills generally. They compose; they do not replace each other.
