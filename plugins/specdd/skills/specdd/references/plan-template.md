# Plan Template

The plan answers **how**. Built only after the spec is signed off. Under 2 minutes to read — if longer, the feature is too big; split it.

---

## Quick variant (Feature scope, inline in chat)

```
**Plan — <feature name>**
- **Stack:** <only if non-obvious — e.g., new dependency>
- **Files:** <new and changed, with one-line purpose each>
- **Key decisions:** <2–4 bullets, each with one-line rationale>
- **Risks:** <anything that might bite>
```

---

## Full variant (Project scope, as a file)

```markdown
# Plan: <feature name>

> Spec: [link to spec.md]

## Approach
One paragraph: overall shape, architecture in a sentence, data flow, where state lives.

## Stack
List anything non-default for this codebase. Skip what's standard.
- **New dependencies:** <name@version + why>
- **No new infra needed** OR **New infra:** <what + why>

## File-level breakdown

### New files
- `path/to/file.ext` — <one-line purpose>

### Changed files
- `path/to/existing.ext` — <what changes and why>

### Data model changes (if any)
- New table / collection: `<name>` — columns, indexes, constraints
- Modified: `<name>` — what changes, migration approach

## Key technical decisions
One line of rationale each.
- **<Decision>:** <one-line rationale>

Worth recording: state management, auth/permission enforcement layer, error handling boundary, caching strategy, validation layer.

## Alternatives considered
One line each. Rejected alternatives show you thought about it.
- **<Alternative>:** rejected because <one line>

## Rollout (only if non-trivial)
- **Migration needed?** <yes/no, approach>
- **Backward compatible?** <yes/no>
- **Feature flag?** <yes/no>
- **Deployment order:** <if multi-service>

## Risks
- **Risk:** <what> — **Mitigation:** <how>
- **Unknown:** <what we'd need to find out>

## Estimated effort
**XS / S / M / L / XL** — and the reasoning if non-obvious.
```

---

## Authoring rules

- **Decisions, not narration.** "We will use X" beats "We are considering many options".
- **One-line rationales.** If you need a paragraph, the choice is probably wrong or the spec is unclear.
- **Surface trade-offs.** When two approaches both work, name them, name the trade-off, recommend one.
- **Flag the boring stuff.** Migrations, env vars, secrets, feature flags. This is where deployments break.
- **Don't pre-code.** Plans describe shapes and decisions. Pseudocode for tricky logic is fine; full implementations aren't.

## Sign-off

*"Plan looks good? Anything to adjust before I build?"* For Project scope, confirm the task breakdown direction before generating `tasks.md`.
