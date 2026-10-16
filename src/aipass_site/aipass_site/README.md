# AIPASS_SITE

**Resident project agent and manager of the `aipass-site` project.**

**Module:** `aipass_site` | **Class:** manager | **Created:** 2026-07-20

---

## What I Do

- Manage this project as its resident agent (citizen_class: manager)
- Coordinate project work and maintain project context across sessions
- Route commands to auto-discovered modules — *scaffolding only today, see Current State*

---

## The Project I Manage

`aipass-site` is the AIPass public landing page — a **static site** (HTML/CSS/JS,
no build step, no framework). It started from the
[LaunchKit](https://launchkit.evilmartians.io) template and has since been
rewritten as the AIPass front door.

Repo root layout (verified 2026-08-25):

```
index.html           # the landing page — 327 lines, AIPass content
logo-preview.html    # branding scratch page
css/                 # index.css, tablet.css, mobile.css, pricing.css
js/                  # main.js, pricing.js
fonts/               # Inter (woff2), JetBrains Mono (ttf)
images/              # AIPass logo/wordmark/favicon + LaunchKit demo assets
vendor/              # Font Awesome 6.7.2
src/aipass_site/     # this agent
```

Live page sections: Hero, What you get, How it works, BYOP, FAQ, CTA.
No "Lorem ipsum" remains in `index.html`.

**Known loose ends (not fixed, reported):**
- The **repo-root `README.md` is still the upstream LaunchKit template readme.**
  It describes LaunchKit, not AIPass — the project's front door misrepresents
  the site that ships. Awaiting GO before touching it.
- `css/pricing.css` and `js/pricing.js` are LaunchKit leftovers — no page in the
  repo references them.

---

## Quick Start

```bash
# Confirm the agent is alive
drone @aipass_site hello

# Show the agent's self-map (modules, help pointer)
drone @aipass_site

# Full help text
drone @aipass_site --help
```

---

## Commands

All commands run through `drone @aipass_site <command>`.

```bash
drone @aipass_site                # Introspection — title, purpose, module list, help pointer
drone @aipass_site hello          # Confirm the agent is alive
drone @aipass_site --help         # Full help text (also -h, help)
```

There is **no `--version` flag** — it is not implemented in the entry point.

---

## Current State

The agent is **scaffolding**: the entry point, discovery, and routing all work,
but nothing is plugged into them yet.

- `apps/modules/` — 0 command modules (only an empty `__init__.py` + README)
- `apps/handlers/` — 0 handlers (only an empty `__init__.py` + README)

So `drone @aipass_site` prints no module list, and `--help` lists only `hello`.
Both are correct output for an empty `modules/` directory — drop a `.py` file
with a `handle_command()` function into `apps/modules/` and it appears
automatically in both.

---

## Architecture

```
apps/
├── aipass_site.py             # Entry point — 163 lines: CLI routing, discovery, introspection, help
├── modules/                   # Business logic (auto-discovered) — empty
└── handlers/                  # Implementation details — empty
```

### Three-Layer Design

1. **Entry point** (`aipass_site.py`) — routes CLI commands; imports no modules or
   handlers directly, it discovers them at runtime
2. **Modules** (`modules/`) — business logic coordinators; each exposes
   `handle_command(command, args)` and optionally a `COMMAND` name
3. **Handlers** (`handlers/`) — implementation details, pure functions where possible

### Discovery

`discover_modules()` globs `apps/modules/*.py`, skips `_`-prefixed files, imports
each (trying `aipass.aipass_site.apps.modules.<stem>` then `apps.modules.<stem>`),
and keeps those exposing `handle_command()`. Import failures are logged via prax
and skipped — they never crash the CLI. `route_command()` then offers the command
to each module in turn until one returns truthy; otherwise the CLI prints
`Unknown command` and exits 1.

---

## Integration

### Depends On

- **`aipass.prax`** — logging via `from aipass.prax import logger`
  (`logger.error` / `logger.warning`)
- **`aipass.cli`** — console output via
  `from aipass.cli.apps.modules import console`; `console` is a `rich.console.Console`
  and only `console.print()` is used

---

*Created by `aipass new` via spawn project_agent template.*

*Every claim above was verified against the code on 2026-08-25.*

*Last Updated: 2026-08-25*
