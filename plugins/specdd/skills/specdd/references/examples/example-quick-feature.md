# Example — Quick-scope feature

A worked example of how the Quick path looks in practice. Total interaction: one round of questions, an inline mini-spec, a thumbs-up, then build.

---

## User says

> "add a copy-link button to the share menu"

## Agent's triage

- Skip check: no, this is a feature
- Scope: **Quick** — single component, no new surface, ~15 min of work
- Existing spec: none
- Surface: Claude Code in a Next.js repo

## Agent's response

> Quick one. Two checks before I build:
>
> 1. **Copies the current page URL, or a custom shareable link with tracking params?**
>    - [ ] Current URL as-is
>    - [ ] Add UTM params (`utm_source=share`)
>    - [ ] Use a server-generated short link
>
> 2. **What's the confirmation when they click?**
>    - [ ] Inline checkmark on the button (replaces icon for 2s)
>    - [ ] Toast: "Link copied"
>    - [ ] Nothing
>
> Assumptions I'll apply unless you flag otherwise: button is keyboard-accessible, focus stays on the button after copy, falls back gracefully if clipboard API is blocked (shows the URL in a text field for manual copy).

## User says

> "1: current URL, 2: inline checkmark"

## Agent's mini-spec

> **Spec — Copy-link button**
> - **User:** Anyone viewing a shareable page wants to copy the URL so they can paste it elsewhere.
> - **Done when:** Button is visible in the share menu; click copies `window.location.href`; icon swaps to checkmark for 2s; works on keyboard.
> - **Edge cases:** If clipboard API is unavailable / blocked, show the URL in a read-only text field with select-all behavior. If clipboard write fails, surface inline error: "Couldn't copy — select and copy manually." with the text field shown.
> - **Out of scope:** UTM tagging, short links, sharing to specific apps (those are separate features).
>
> Building now.

## Agent builds

Implements the component. Runs the relevant subset of the production-grade checklist:

- Loading: N/A (instant)
- Empty: N/A
- Error: clipboard failure path covered
- Keyboard: button is `<button>`, focusable, activates on Enter / Space
- Focus: stays on button after click
- Touch target: 44×44px confirmed
- a11y: `aria-label="Copy link"` on the button, `aria-live="polite"` region announces "Link copied" on success

## Agent's done message

> Done. Copy-link button is in `components/share-menu.tsx`. Verified keyboard, focus, and the clipboard-blocked fallback. Did not test screen reader behavior end-to-end — you may want to check that the `aria-live` announcement reads correctly in your target screen reader.

---

## What this example shows

- **Tight interview** — 2 tappable questions, not a form.
- **Assumptions stated up front** — gives the user a chance to override the defaults the skill bakes in.
- **Mini-spec inline** — 5 lines, but every section that matters is there.
- **No tech in the spec** — `window.location.href` shows up only when building, not when speccing.
- **Honest verify report** — what was checked vs what wasn't.

This is the bar for a Quick-scope flow. Total agent turns: ~3. Total user effort: tap two options once.
