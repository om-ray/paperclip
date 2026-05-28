# mstack — goal-to-completion workflow

This project uses [mstack](https://github.com/alnimra/mstack) for managing
goals end-to-end via a GitHub parent-issue ledger.

## How any agent can use it

Whether you're driving via Claude Code, Codex CLI, Gemini CLI, Cursor, Aider,
or any other agent that can shell out, the workflow is the same:

1. Compile a plan:
   ```
   mstack plan
   # edit MSTACK_PLAN.md, then:
   ```
2. Publish to GitHub as the canonical ledger:
   ```
   mstack publish
   ```
   This creates one parent issue (label `mstack:goal`) + one sub-issue per task.

3. Drive implementation from the parent issue:
   ```
   mstack implement
   ```
4. Transition stages as you progress:
   ```
   mstack stage IMPLEMENTING --note "starting T1"
   mstack stage REVIEW_READY --note "PR up at #123"
   mstack stage DONE
   ```
5. Read / update managed blocks directly:
   ```
   mstack ledger read --block resume-here
   mstack ledger write --block resume-here < new_content.md
   ```

## Source of truth

After `mstack publish`, the **GitHub parent issue is the source of truth.**
Local artifacts (`MSTACK_PLAN.md`, `.mstack/`) are provenance/cache only.

## Managed blocks

The parent issue body contains machine-edited blocks. Do not hand-edit between
the `<!-- mstack:NAME:start -->` and `<!-- mstack:NAME:end -->` markers:

- `stage-ledger`
- `resume-here`
- `plan-summary`
- `task-map`
- `handoff`
- `completion-gates`

Humans can freely edit outside those blocks.
