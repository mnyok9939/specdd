# Example — Feature-scope flow

A worked example of a Feature-scope flow: full spec + plan, but no separate tasks file. Typical for 1–4 hours of work.

---

## User says

> "i want to let users export their notes to markdown"

## Agent's triage

Feature scope — 1–3 hours, new flow, touches existing data. Claude Code in a Next.js + Supabase app.

## Agent's interview (one round)

> A few things before I draft the spec:
>
> 1. **What's "all notes"?**
>    - [ ] Currently selected note only
>    - [ ] All notes in the active folder
>    - [ ] All notes the user owns (full export)
>    - [ ] Let the user choose
>
> 2. **One file or many?**
>    - [ ] One `.md` per note, zipped
>    - [ ] All notes concatenated into a single `.md`
>    - [ ] Both options available
>
> 3. **Images** — embed inline or just leave references?
>
> Defaults I'll apply unless flagged: filename per note is sluggified title; front-matter with `title`, `created_at`, `updated_at`, `tags`; export is async to handle large accounts.

## User says

> "all notes user owns, zipped one-per-note, images inline as base64. async makes sense, accounts have thousands of notes"

## Agent's spec (shape only — see `spec-template.md` for full structure)

The spec covers:

- **Summary** — async export of all owned notes as a ZIP of per-note `.md` files with front matter and base64 images
- **User stories** — one: backup / portability
- **Acceptance criteria** — 7 checkable items (trigger from Settings, progress UI, download link, ZIP structure, front-matter fields, 24h expiry, retry on failure)
- **States** — Idle / In progress / Ready / Failed / Expired
- **Edge cases** — zero notes, double-trigger, image fetch failure, account deletion mid-export
- **Out of scope** — import, partial export, other formats, scheduled exports (named explicitly to prevent creep)
- **Non-functional** — perf budget (1000 notes in 2 min), 24h signed URL TTL, structured logs

## Agent's plan (shape only — see `plan-template.md` for full structure)

The plan covers:

- **Approach** — background job, streaming ZIP to storage, signed URL with 24h expiry
- **Stack** — adds `jszip` and Markdown emit library; uses existing storage + email + realtime
- **Files** — settings UI, API route, archive builder, worker entry, email template, types
- **Data model** — new `note_exports` table tracking status, expiry, storage path
- **Key decisions** — streaming (not in-memory) ZIP, base64 inline images, one job per user at a time, signed URLs not public
- **Alternatives considered & rejected** — synchronous export, scheduled cleanup cron, image-to-blob
- **Risks** — large-account OOM (mitigated by streaming); base64 inflates size (accepted trade-off)
- **Effort** — M (~3 hours)

## Agent's confirmation

> Spec and plan above. The big choices: streaming ZIP (handles "thousands of notes"), base64 images (portability requirement), 24h expiring download links. Any changes before I build?

## User says

> "ship it"

## Agent builds

Implements in order: migration → worker → API route → UI → email. Commits per logical unit. Runs production checklist before declaring done.

---

## What this example shows

- **One interview round** got everything needed.
- **Spec is tech-free** — no mention of `jszip` or `base64` until the plan.
- **Plan is dense** — under 2 minutes to read, every decision has a one-line rationale.
- **All five states addressed** explicitly.
- **Edge cases listed** before they could bite.
- **Out-of-scope is aggressive** — prevents "but I also wanted PDF" later.
