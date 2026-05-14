# specdd

> **Spec-Driven Development as a single Agent Skill.** Drop it in, type naturally, ship features that don't embarrass you in two weeks.

specdd turns vague, top-of-mind feature requests into production-grade specs **before** code is written — without a CLI, without four config files, without ceremony you don't need. One skill, any modern AI coding agent: Claude (Code, Desktop, Web), Codex, Copilot, Cursor, Windsurf, Gemini CLI, anything else that reads `SKILL.md` or `AGENTS.md`-style instructions.

```
You: "build me a settings page where users can change their email"

specdd:
  → triages the scope (Feature)
  → asks the 2-3 questions you didn't think to address (verification email?
    active sessions? what's the success state?)
  → produces a tech-free spec + a 2-minute technical plan
  → only after you say "ship it" → writes code
  → runs the production-grade checklist before declaring done
```

No `npx`, no `uv tool install`, no `specify init`. Just a folder.

---

## Why specdd exists

Two patterns broke the same way:

**Vibe-coding** — describe a feature in one line, get code that compiles and looks right but misses the empty state, the error state, the keyboard handling, the "what happens when the user double-clicks the button" — discovered in production.

**Heavy spec frameworks** like [github/spec-kit](https://github.com/github/spec-kit) — fix the rigor problem but introduce a CLI, four mandatory artifacts, and ceremony that's overkill for solo and one-off work.

specdd splits the difference. Spec-driven development that **scales down to a 15-minute task** and **scales up to a multi-day project** — same workflow, different ceremony.

---

## What you get

- **One opinionated workflow** — triage → interview → spec → plan → (tasks) → build & verify
- **Question-asking by default** — interviews you for the gaps your one-liner left, instead of guessing
- **Tech-free specs** — what & why for the user, separated from how for the agent
- **Production-grade checklist** before "done" — empty/error/loading states, a11y, keyboard, mobile, observability
- **UX defaults baked in** — five-states rule, confirmation patterns, optimistic updates, accessible focus management
- **Scales to scope** — Quick (5-line inline mini-spec), Feature (spec + plan inline), Project (spec + plan + tasks as files)
- **Surface-agnostic** — same skill in Claude Code, Claude.ai, Codex CLI, Cursor, Copilot, Windsurf

---

## Install

### Claude Code (recommended)

```bash
/plugin marketplace add unboundinnov/specdd
/plugin install specdd@specdd
```

That's it. The skill activates automatically when you ask for any feature work.

### Claude Code (manual, no plugin system)

```bash
git clone --depth=1 https://github.com/unboundinnov/specdd /tmp/specdd-src
cp -r /tmp/specdd-src/plugins/specdd/skills/specdd ~/.claude/skills/
rm -rf /tmp/specdd-src
```

Or scope to a single project: copy into `.claude/skills/` inside the project instead.

### Claude.ai (Pro / Team / Enterprise / Max)

1. Download `specdd.zip` from [Releases](../../releases) (or zip `plugins/specdd/skills/specdd/`).
2. Claude.ai → **Settings → Capabilities → Skills → Upload skill**.
3. Upload the zip.

### Codex CLI

```bash
mkdir -p ~/.codex/skills
git clone --depth=1 https://github.com/unboundinnov/specdd /tmp/specdd-src
cp -r /tmp/specdd-src/plugins/specdd/skills/specdd ~/.codex/skills/
rm -rf /tmp/specdd-src
```

### Cursor / Copilot / Windsurf / Aider / others

These agents don't natively load `SKILL.md` yet. Copy the content of [`SKILL.md`](./plugins/specdd/skills/specdd/SKILL.md) into the agent's instructions file:

- **Cursor:** `.cursor/rules/specdd.mdc` (or legacy `.cursorrules`)
- **GitHub Copilot:** `.github/copilot-instructions.md`
- **Windsurf:** `.windsurfrules`
- **Aider:** `CONVENTIONS.md` referenced from `.aider.conf.yml`

Reference files in [`references/`](./plugins/specdd/skills/specdd/references/) can be copied alongside or inlined.

---

## How it works

| Phase | What happens |
|---|---|
| **1. Triage** | Skip / Quick / Feature / Project — surfaced so you can correct it. |
| **2. Interview** | 2–5 right questions for your request type, tappable where possible. Doesn't ask what it can infer. |
| **3. Spec** | Tech-free: who / what / why / states / edge cases / out-of-scope / non-functional. You sign off. |
| **4. Plan** | Tech approach: stack, files, decisions with rationale, alternatives, risks. <2 minutes to read. |
| **5. Tasks** | (Project scope only) Ordered, verifiable units with explicit done-signals. |
| **6. Build & verify** | Implement against spec; deviations require a spec update. Production checklist before "done". |

[`SKILL.md`](./plugins/specdd/skills/specdd/SKILL.md) is the entry point; templates, checklists, and examples are in [`references/`](./plugins/specdd/skills/specdd/references/).

---

## specdd vs spec-kit

| | specdd | [github/spec-kit](https://github.com/github/spec-kit) |
|---|---|---|
| **Install** | Copy a folder, or one `/plugin install` | `uv tool install`, `specify init`, CLI per-project |
| **Surface** | Any agent that reads `SKILL.md` / instructions | 30+ agents via Specify CLI |
| **Ceremony** | Scales: 5 lines for a small change, 3 files for a project | Mandatory: `constitution.md`, `spec.md`, `plan.md`, `tasks.md` |
| **Slash commands** | None — conversational | `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement` |
| **UX defaults** | Baked in (5-states rule, a11y, confirmation patterns, motion) | Project-defined in `constitution.md` |
| **Best for** | Solo, indie, one-off features, mid-size teams | Larger teams, established projects, formal SDD adoption |

**What specdd inherits from SDD literature (and spec-kit):** the `spec → plan → tasks` workflow shape, the `spec.md` / `plan.md` / `tasks.md` filenames, the "tech-free spec" framing. These are general SDD concepts (Spec Driven Development pre-dates spec-kit), and keeping the filenames means specs migrate cleanly if you ever adopt spec-kit later.

**What's specdd's own:** the triage step (scale to scope), the interview phase with tappable options, the build & verify phase with the production-grade checklist, UX-first opinionation with the five-states rule, the common-sense gates. No CLI, no slash commands, no constitution.

---

## Examples

See [`references/examples/`](./plugins/specdd/skills/specdd/references/examples/):

- [`example-quick-feature.md`](./plugins/specdd/skills/specdd/references/examples/example-quick-feature.md) — Quick scope (~15 min of work)
- [`example-feature-spec.md`](./plugins/specdd/skills/specdd/references/examples/example-feature-spec.md) — Feature scope (~3 hours of work)
- [`example-project.md`](./plugins/specdd/skills/specdd/references/examples/example-project.md) — Project scope (multi-day)

---

## Contributing

Issues and PRs welcome. Particularly interested in:

- Request-type interview playbooks (the more specific, the better)
- Surface-specific install instructions for new agents
- Worked examples from real projects

Open an issue first for substantial changes; keep PRs focused; match the existing tone.

---

## License

MIT. See [LICENSE](./LICENSE).

---

## Credits

Inspired by, and respectfully different from, [github/spec-kit](https://github.com/github/spec-kit), [BMAD](https://github.com/bmadcode/BMAD-METHOD), and [Kiro](https://kiro.dev/). Built on the [Agent Skills format](https://github.com/anthropics/skills) by Anthropic.

If specdd helps you ship better, a ⭐ helps people find it.
