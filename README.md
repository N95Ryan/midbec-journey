
<div align="center">
  <img src="assets/profile.jpg" alt="Ryan Pina-Silasse" width="500" style="border-radius:50%" />

  # 🧭 My Midbec Journey

  A public engineering journal documenting a solo platform modernization from legacy infrastructure to a modern full-stack architecture.
  
  One scope at a time.

  [![LinkedIn](https://img.shields.io/badge/LinkedIn-Ryan%20Pina--Silasse-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ryan-pina-silasse/)
</div>

---

## 🎯 The Mission

Midbec is a Canadian industrial parts distributor based in Drummondville, QC. I joined as the **sole developer** with one objective: modernize a platform that hadn't changed in decades.

The scale:
- **500K → 2M+ parts** in the product catalog
- **Zero existing frontend architecture** — starting from scratch
- **One developer** — full ownership over architecture, stack decisions, and delivery

This repo is where I document the journey publicly, day by day.

---

## 📊 Impact (in progress)

| Metric | Before | After |
|---|---|---|
| Lighthouse Performance | 55 | TBD |
| Lighthouse Accessibility | 71 | TBD |
| Lighthouse Best Practices | 96 | TBD |
| Lighthouse SEO | 100 | TBD |
| First Contentful Paint | 2.5s | TBD |
| Total Blocking Time | 4,380ms ⚠️ | TBD |

> Baseline measured pre-Bootstrap/SCSS removal. Scores will be updated post-migration.

---

## 🗂️ How to navigate this repo

```
midbec-journey/
├── 01 - Context/
│   ├── mission.md
│   ├── stack.md
│   └── unopim-roadmap.md   # UnoPIM integration roadmap (Cursor reference)
├── 02 - The Team/          # Collaborators, roles, working dynamics
├── 03 - Daily Logs/        # Day-by-day engineering log (YYYY-MM/YYYY-MM-DD.md)
└── .cursorrules            # Enforces consistent note format across the vault
```

**Recommended reading order:**
1. [`01 - Context/`](./01%20-%20Context/) — mission, stack, and architecture decisions
2. [`unopim-roadmap.md`](./01%20-%20Context/unopim-roadmap.md) — current catalogue integration (UnoPIM)
3. Pick any daily log in [`03 - Daily Logs/`](./03%20-%20Daily%20Logs/) — see the work in practice
4. Check the scopes table below — track overall progress

---

## 🔄 Delivery Scopes

| # | Scope | Status |
|---|---|---|
| 1 | Homepage components (Header, Footer, Slider, Featured Products…) | ✅ Done |
| 2 | Tailwind CSS migration — SCSS/Bootstrap removal (homepage layer) | ✅ Done |
| 3 | Mobile responsive — hamburger menu, full mobile component migration | ✅ Done |
| 4 | Auth end-to-end (Next.js ↔ Go API, session hydration, CORS proxy) | ✅ Done |
| 5 | Account dashboard (addresses, orders, invoices, profile, password) | ✅ Done |
| 6 | i18n routing — bilingual URLs (FR/EN) with next-intl | ✅ Done |
| 7 | Garage/Vehicle feature removal — full cleanup | ✅ Done |
| 8 | PartSmart integration — model search, IPL exploded view, cart | ✅ Done |
| 9 | Unified header search — autocomplete + `/recherche` page (part mode) | ✅ Done (code — catalog results empty until Patrick's import) |
| 10 | UnoPIM — OAuth2 auth, category cache, Go proxy | ✅ Done |
| 11 | UnoPIM — category tree, icons, dynamic catalogue menu | ✅ Done |
| 12 | UnoPIM — product listing + unified navigation + drill-down panel | ✅ Done |
| 13 | UnoPIM — header search (ERP discovery + PIM enrichment) | ✅ Done (code — Patrick's product import in progress) |
| 14 | Interim ERP catalog + product detail page E2E + shop cleanup Phase 1 | ✅ Done |
| 15 | ERP catalog UX polish (title-case, leaf megamenu) + minimal CI/CD | ✅ Done (Jun 19) |

> Scopes 10–13 map to steps 0→3 in [`unopim-roadmap.md`](./01%20-%20Context/unopim-roadmap.md). Scope 13 is delivered on the code side; part autocomplete remains empty until ERP SKU ↔ UnoPIM alignment. **Active catalog: interim ERP** (`NEXT_PUBLIC_CATALOG_SOURCE` unset) pending UnoPIM unblock.

---

## 🛠️ Stack

Full details in [`stack.md`](./01%20-%20Context/stack.md).

| Layer | Tech |
|---|---|
| Frontend | Next.js 15 (App Router) · React 19 · TypeScript 5.8 · Tailwind CSS v4 |
| Backend | Go · Chi · PostgreSQL |
| PIM | UnoPIM (product source of truth) |
| Data fetching | TanStack Query v5 |
| i18n | react-intl (FR / EN) |
| Infra | LXC containers · GitLab CI/CD |
| Package manager | Bun |

---

## 🧠 The approach

Each daily log follows a consistent format:

- **Mood & context** — a human note on the day
- **Goals** — what was planned
- **Completions** — what was actually done, with enough detail to reconstruct the reasoning
- **What I learned** — one generalizable principle extracted from the day's work
- **Watch points** — traps, gotchas, things to watch
- **Next steps** — what's queued
- **Energy** — one sentence on the day's state

A few principles that show up repeatedly across the logs:

- **Audit before touching anything** — `grep`/`cat` before every change, every time
- **Atomic commits** — `git diff --stat` before every push, one logical unit per commit
- **Deletion order matters** — learned the hard way: removing an SCSS import after the file breaks React hydration silently
- **Strangler fig over big bang** — the Go API migration runs in parallel with the legacy layer, not as a replacement
- **YAGNI enforced** — features built on confirmed need, not speculation

---

## 📝 Notes

- Logs are written in French (my working language at Midbec)
- This repo is a signal of *engineering approach*, not a technical specification
- **Privacy policy for public logs:**
  - Never secrets, tokens, emails, or partial OAuth/client identifiers
  - Environment variable **names** are OK; **values** are never written
  - Colleagues may be named; their emails may not
  - Mood and context notes are intentional — see [`.cursorrules`](./.cursorrules)

---

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Ryan%20Pina--Silasse-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ryan-pina-silasse/)

*Drummondville, QC*

</div>