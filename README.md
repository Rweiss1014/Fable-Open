# Fable-Open

An orchestrator skill for [Claude Code](https://claude.com/claude-code).

It puts the main agent in the role of a lead orchestrator: plan the work, route
each piece to the right model, review what comes back, integrate it, and decide
when the work is actually done. Subagents execute bounded missions. The
orchestrator plans, routes, reviews, and decides.

## What it changes

Without it, an agent handed a large task tends to start editing files and keep
going until something looks finished. With it, the agent:

- Understands the outcome and inspects the existing system **before** changing it
- Breaks the request into bounded workstreams with explicit scope, boundaries,
  and acceptance criteria
- Routes by cost and difficulty - Haiku for reconnaissance, Sonnet for building,
  Opus for hard engineering, fresh-context Opus for independent verification
- Runs independent work in parallel while avoiding overlapping writes
- Refuses to accept "done" as evidence of completion
- Escalates on repeated failure instead of retrying the same approach louder
- Protects the existing product from unrequested refactors and rewrites

## Install

Drop it in your user skills directory so every project on the machine can use it:

```bash
git clone https://github.com/Rweiss1014/Fable-Open.git ~/.claude/skills/fable-open
```

On Windows (PowerShell):

```powershell
git clone https://github.com/Rweiss1014/Fable-Open.git "$env:USERPROFILE\.claude\skills\fable-open"
```

Project-scoped instead of global? Clone it into `.claude/skills/fable-open`
inside the repo.

Verify Claude Code sees it by running `/fable-open` in a session, or asking
"what skills do you have".

## Use

Invoke it explicitly with `/fable-open`, or let Claude load it on its own -
the skill description triggers on substantial multi-step work, parallel
workstreams, large investigations, migrations, audits, and high-risk changes
that need independent verification.

Do not reach for it on tiny edits, single-file fixes, or conversational
questions. Orchestration has a coordination cost, and the skill says so itself:
delegate when delegation creates value, not merely because you can.

## Layout

```
fable-open/
  SKILL.md    the doctrine - routing, delegation gate, escalation,
              review, verification, completion standard
  README.md
  LICENSE
```

Everything lives in `SKILL.md`. Fork it and tune the routing table to your own
model mix.

## License

MIT
