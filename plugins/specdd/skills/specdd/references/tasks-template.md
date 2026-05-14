# Tasks Template

Tasks break a Plan into ordered, independently completable units. Only generate a `tasks.md` for **Project scope** (multi-day work). For Quick or Feature scope, the agent's todo list is enough.

Each task should be small enough that a single agent turn can complete and verify it. If a task feels like "and also...", split it.

---

## File format

```markdown
# Tasks: <feature name>

> Spec: [link to spec.md]
> Plan: [link to plan.md]

## Conventions
- Tasks are ordered. Don't skip ahead unless a dependency is independently met.
- Each task has an observable "done" signal.
- Mark `[x]` completed, `[~]` in progress, `[ ]` not started.

## Task list

### Setup & scaffolding
- [ ] **T1: <task name>**
  - **Does:** <one-line outcome>
  - **Files:** <files touched>
  - **Done when:** <observable signal>
  - **Depends on:** <task IDs or "nothing">

### Core implementation
- [ ] **T2: ...**

### Edge cases & states
- [ ] **T3: Empty state for <X>**
- [ ] **T4: Error state for <X>**
- [ ] **T5: Loading state for <X>**

### Polish & verify
- [ ] **TN: Run production-grade checklist**
- [ ] **TN+1: Accessibility pass**

## Notes log
Record decisions, surprises, or spec revisions as you build.
- **YYYY-MM-DD:** ...
```

---

## What makes a good task

**Good:**
- "Add `users` table with `id`, `email`, `created_at`. Done when migration applies cleanly to a fresh DB."
- "Render the inbox empty state — illustration, headline, primary CTA. Done when visible on `/inbox` with no messages."

**Bad** (too big, too vague, or no done-signal):
- "Build the user system." (huge)
- "Make it work." (vague)
- "Improve performance." (no done-signal)

If a task description doesn't fit in a sentence, it's two tasks pretending to be one.

## Ordering

Scaffolding before features. Data before UI. Happy path before edges. Verify last. When in doubt, ship the thinnest end-to-end slice first, then thicken it.
