# Production-Grade Checklist

The boring-but-critical pass. Run **before** declaring a feature done. The difference between "compiles and runs" and "delightful in production" is in this list.

Not all items apply to every feature — skip what's irrelevant, but be honest about what you skipped.

## UX states

- [ ] **Loading** — feedback within 100ms of any action. Skeleton for content >300ms; spinner only for short in-context loads.
- [ ] **Empty** — first-time / no-data state has a primary action and explains what fills this space.
- [ ] **Error** — actionable message with retry / recovery path. "Something went wrong" alone is not acceptable.
- [ ] **Partial** — what happens when some-but-not-all data loaded? (e.g., 3 of 10 items errored)
- [ ] **Success** — visible, dismissable confirmation; doesn't block the next action.
- [ ] **Offline** — if feature touches network, what happens offline? At minimum surface the state.
- [ ] **Slow network** — works on 3G; loading states actually appear.

## Inputs & forms

- [ ] **Validation on blur** (not keystroke), inline at the field, not toast-only.
- [ ] **Edge inputs handled** — empty, very long, unicode, emoji, leading/trailing whitespace, special chars (`<>&"'`), zero, negative, very large numbers, future/past dates.
- [ ] **Required vs optional** clear before submission.
- [ ] **Sensible defaults** pre-filled where possible.
- [ ] **Failed submit** scrolls to and focuses the first invalid field.
- [ ] **Submit button** shows progress ("Saving…") and disables while in flight.
- [ ] **`autocomplete`** attribute set correctly (`email`, `current-password`, `new-password`, `name`).

## Destructive actions

- [ ] **Confirmation** on delete / overwrite / bulk-edit / send / publish. Pattern scales with impact: undo toast → modal → type-the-name.
- [ ] **Undo window** preferred over modals for reversible actions.
- [ ] **No accidental triggers** — destructive buttons not visually dominant; not adjacent to common-path buttons.

## Concurrency

- [ ] **Double-submit prevented** — button disables after click, OR requests are idempotent.
- [ ] **Race conditions handled** — fast double-click, navigate-during-save, two-tab editing.
- [ ] **Stale data** — how do users find out if data changed server-side while they viewed it?

## Auth, permissions, privacy

- [ ] **Auth check on every protected route / endpoint**, server-side (not just hidden in UI).
- [ ] **Permission check** — respects who-can-do-what.
- [ ] **No sensitive data in URLs, logs, or client bundles.**
- [ ] **Tokens / secrets** never logged, never in error messages surfaced to users.
- [ ] **PII** only collected if needed, only shown to those who should see it.

## Accessibility (WCAG AA floor)

- [ ] **Keyboard navigable** — every interactive element reachable; logical tab order.
- [ ] **Focus visible** — never `outline: none` without replacement.
- [ ] **Focus management** — modals trap focus and return on close; route changes move focus to new content.
- [ ] **Screen reader** — landmarks (`<main>`, `<nav>`), heading order, `alt` on images, `aria-label` on icon-only buttons.
- [ ] **Color contrast** — AA (4.5:1 normal, 3:1 large). Don't rely on color alone.
- [ ] **Reduced motion** — respect `prefers-reduced-motion: reduce`.
- [ ] **Form fields** — every `<input>` has a `<label>`; errors linked via `aria-describedby`.

## Responsiveness

- [ ] **Mobile** — usable at 360px. Touch targets ≥44×44px. No horizontal scroll.
- [ ] **Zoom** — usable at 200% browser zoom (WCAG AA requirement).
- [ ] **Touch vs mouse** — hover-only interactions have a touch equivalent.

## Performance

- [ ] **Initial load** within spec budget (default LCP <2.5s, INP <200ms).
- [ ] **No obvious bundle bloat.** New dependencies justified.
- [ ] **No N+1s** in list views.
- [ ] **Images** — appropriate size/format; lazy-loaded below the fold.
- [ ] **No cascading re-renders** on keystroke in large lists.

## Observability

- [ ] **Errors logged** with enough context to debug (request ID, user ID where allowed, stack).
- [ ] **Key events instrumented** for the metric the feature is supposed to move.
- [ ] **No noisy logs** in normal flow.

---

## How to use

1. **Don't apply blindly.** A 10-line bug fix doesn't need all of this.
2. **Run it once before declaring done.** Walk through, check or skip each item.
3. **Be honest in the report.** *"Verified items 1–15, skipped i18n (single-locale), didn't test screen-reader behavior."* is the right level of disclosure.
4. **Many skips → ask why.** A pattern of skips often means the feature isn't really done.
