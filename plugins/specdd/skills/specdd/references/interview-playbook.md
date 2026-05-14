# Interview Playbook

How to ask the right questions, organized by request type. **Pick 2–5 questions total — never run the full list.** Questions are ordered most-to-least important; start at the top.

When tappable options are available, prefer them over open-ended questions — faster on mobile, surfaces options users may not have considered.

---

## Universal opener (any request type)

Before reaching for a section below, run these gap-fillers if the user hasn't already answered them:

1. **Who is this for?** (end users, internal team, just you, a specific persona)
2. **What's the smallest version that ships?** (forces MVP thinking)
3. **What is explicitly out of scope?** (prevents creep)

If the user already answered all three, skip straight to a request-specific section below.

You're done interviewing when:
- The spec template's `Acceptance Criteria` section can be filled with concrete, checkable items
- You can describe the happy path AND at least 2 unhappy paths
- You know what's out of scope

If you can't fill those after 2 rounds, the request is too big — split it.

---

## UI / Screen / Component

When the user asks for a screen, page, modal, form, dashboard, or component.

1. **What does the user see first?** (the most prominent element / hero state)
2. **What can they do here?** (primary action vs. secondary actions)
3. **States to cover** — loading, empty, error, success, partial-data, offline. Which apply?
4. **Where does this live?** (new route, modal over existing screen, embedded panel)
5. **Mobile / desktop / both?** Any breakpoints to respect?
6. **Existing pattern to follow?** (a similar screen, or a reference design)

---

## CRUD feature (Create / Read / Update / Delete)

1. **What's the resource?** (e.g., "tasks", "team members") — name and key fields
2. **Who can do what?** (auth/permission — owner only, team, public)
3. **Create flow** — inline / modal / dedicated page? Auto-save or submit?
4. **Delete behavior** — soft or hard? Confirmation pattern? Undo window?
5. **List view** — pagination, infinite scroll, fixed? Sort/filter needs?
6. **Bulk actions?** (select multiple, bulk delete/edit)

---

## API / Backend endpoint

1. **Caller** — own frontend, third party, internal service, agent?
2. **Auth** — public, authenticated, role-gated?
3. **Request / response shape** — happy path, then error shape
4. **Idempotency** — is repeated submission safe? (matters for payments, sends, creates)
5. **Validation** — what's required, what's optional, what are the constraints?
6. **Pagination / filtering / sorting** if list-returning

---

## Integration / Third-party

When connecting to an external service (payment provider, Slack, an API, etc.).

1. **Trigger** — user action, schedule, webhook from the other side?
2. **Data flow** — read-only? write? both?
3. **Auth model** — API key, OAuth, service account? Who provides credentials?
4. **Failure behavior** — what if the third party is down or slow? Retry / queue / surface error?
5. **Rate limits / quotas** known?
6. **Webhook security** if applicable (signature verification, replay protection)
