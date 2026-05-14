# Spec Template

The spec answers **what** and **why** — never **how**. No frameworks, libraries, file paths, function names, or implementation details. If a non-technical PM could write it, you're at the right level.

Keep it short. Most specs are under one page.

---

## Quick variant (Quick scope, inline in chat)

For sub-30-minute work, this is enough:

```
**Spec — <feature name>**
- **User:** <who> wants <what> so they can <why>
- **Done when:** <one or two checkable criteria>
- **Edge cases:** <error / empty / loading behavior>
- **Out of scope:** <what we are not doing>
```

5–8 lines. State assumptions inline. Get a thumbs-up, then build.

---

## Full variant (Feature / Project scope)

```markdown
# Spec: <feature name>

## Summary
One paragraph (3–5 sentences) describing what this is, who it's for, and what changes for them after we ship.

## User stories
*As a <role>, I want <capability>, so that <outcome>.*
- As a ..., I want ..., so that ...

Most features have 1–3 stories. One is fine.

## Acceptance criteria
Concrete, checkable items. The feature is done when all are true. Observable by someone other than the implementer, without reading code.
- [ ] ...
- [ ] ...

## User experience

### Happy path
1. User does X
2. System shows Y
3. ...

### States
- **Loading:** ...
- **Empty:** ... (include the primary action available)
- **Error:** ... (what's the recovery action?)
- **Success:** ... (toast, inline, redirect?)
- **Partial / degraded:** ... (if applicable)
- **Offline:** ... (if applicable)

### Edge cases
- Very long / very short / unicode / emoji inputs
- Permission denied / unauthorized
- Concurrent edits by another user (if applicable)
- Slow network (3G or worse)
- Repeated actions / double-submit
- Other domain-specific edges

## Out of scope
Explicitly list what we are NOT doing. As important as what we are.
- ...

## Non-functional requirements
Include only what actually matters for this feature.
- **Accessibility:** WCAG AA minimum unless stated otherwise.
- **Performance budget:** <e.g., perceived load <1s, interaction <100ms>
- **Privacy / security:** <what data, where it goes, who sees it>
- **Observability:** <what events / metrics / errors get logged>
- **Internationalization:** <if relevant>
- **Browser / device support:** <if narrower than app default>

## Open questions / risks
Things you couldn't answer, or things that might bite. Flag them — don't silently pick.
- ...
```

---

## Authoring rules

- **No tech.** No "API endpoint", "React component", "Postgres column". Plan territory.
- **No future-proofing.** Spec what we're building now.
- **Plain language.** A user could read this.
- **Concrete, not aspirational.** "Fast" isn't a spec; "p95 under 200ms" is.
- **Short beats vague.** A 6-line spec that's right beats a 60-line one that's hand-wavy.

## Sign-off

Before moving to the plan: *"Does the spec capture what you want? Anything to add or change?"* Wait for explicit yes. Revisions are normal.
