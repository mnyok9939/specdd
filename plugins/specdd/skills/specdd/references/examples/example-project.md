# Example — Project-scope flow

A worked example of Project scope: spec + plan + tasks as files in `specs/<feature>/`. For multi-day work where the artifacts pay for themselves.

This example sketches the *shape* of Project-scope output. Full content follows the templates in the parent `references/` directory.

---

## User says

> "i want to add a team workspace feature so multiple users can share notes. invites, roles, the whole thing"

## Agent's triage

Project scope — multi-day, touches auth, data model, UI, emails. Writes `spec.md`, `plan.md`, `tasks.md` to `specs/team-workspaces/`. Two interview rounds — high-level shape first, then edges.

## Round 1 — the shape

1. **What's the unit?** — single team / personal+team folders / hybrid
2. **How many teams per user?** — one / many
3. **What roles?** — flat / Owner+Member / Owner+Admin+Member+Viewer

> User picks: hybrid, multiple teams, four roles.

## Round 2 — the edges

1. **Invite flow** — email-only, or shareable invite links too?
2. **Billing implications** — gated by plan, or open to all accounts?
3. **What happens to a member's team-scope notes when they leave?** — stay / revert to personal / member's choice

> User picks: email-only for v1, no billing yet, notes stay with the team.

## Agent writes the files

Creates `specs/team-workspaces/` with three files:

**`spec.md`** — user stories per role; acceptance criteria; UX including invite flow, role management, note movement between personal/team; the five states for each affected screen; edge cases (last owner leaving, invited user already a member, expired invite); out-of-scope explicitly named (billing, SSO, custom roles, audit log) so they don't creep in.

**`plan.md`** — data model (teams, team_members, invites tables); permission enforcement (server-side per-route + RLS policies); UI architecture (team switcher, settings, invite modal); notification approach (email + in-app banner); risks (RLS complexity, invite race conditions).

**`tasks.md`** — ordered list, grouped:

```
### Foundation
- T1: Migration — teams, team_members, invites tables
- T2: RLS policies for team-scoped notes
- T3: Permission helper

### Team CRUD
- T4: Create team API
- T5: List user's teams API
- T6: Team switcher UI
- T7: Team settings page (Owner/Admin only)

### Members & invites
- T8: Create invite API
- T9: Invite email template
- T10: Invite accept flow
- T11: Members list UI
- T12–T14: Role changes, removal, invite modal

### Note movement
- T15: Move note between scopes API
- T16: "Move to..." UI

### Edge cases & states
- T17: Last-owner-leaving prevention
- T18: Expired invite handling
- T19–T21: Empty / loading / error states for new screens

### Polish & verify
- T22: a11y pass
- T23: Production-grade checklist
- T24: Manual end-to-end test with 2 accounts
```

## Spec change mid-build

User reviews, asks: *"actually viewers should be able to comment on notes - not edit but comment."*

Agent updates `spec.md` (adds comment permission to Viewer), `plan.md` (adds comments table), inserts `T15a/T15b/T15c` for comments into `tasks.md`. Surfaces the diff. User confirms.

## Agent works through tasks

In order, marking `[~]` in progress, `[x]` done. Commits per task or per logical group. Updates spec's Notes log when surprises come up. Runs production checklist before T23 is marked done.

---

## What this example shows

- **Two-round interview** — shape first, edges second. Doesn't firehose.
- **Files on disk** — multi-day work earns persistent artifacts.
- **Tasks ladder up to spec criteria** — nothing in tasks that isn't a spec line.
- **Spec changes are formal** — update spec, propagate to plan and tasks, re-confirm.
- **Out-of-scope is aggressive** — billing, SSO, custom roles, audit log all named to prevent creep.

This is the upper bound of specdd ceremony. Anything bigger should be split into multiple Project-scope features.
