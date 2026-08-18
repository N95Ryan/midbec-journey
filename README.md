
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

Technical READMEs live in the code repos — this vault is the **human narrative**, not the API spec.

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
│   ├── mission.md            # Role, timeline, responsibilities
│   └── stack.md              # High-level stack (sync with code READMEs periodically)
├── 02 - The Team/
│   ├── ryan.md
│   └── patrick.md            # Infra / DevOps
├── 03 - Daily Logs/          # Day-by-day log — YYYY-MM/YYYY-MM-DD.md
│   ├── 04 - Mai 2026/
│   ├── 05 - Juin 2026/
│   ├── 06 - Juillet 2026/
│   └── 07 - Août 2026/
├── assets/
└── .cursorrules              # Daily log format + privacy rules for AI agents
```

**Recommended reading order:**
1. [`01 - Context/mission.md`](./01%20-%20Context/mission.md) — why this project exists
2. [`01 - Context/stack.md`](./01%20-%20Context/stack.md) — stack overview (may lag code — see code READMEs)
3. Pick any daily log in [`03 - Daily Logs/`](./03%20-%20Daily%20Logs/) — see the work in practice
4. Check the scopes table below — track overall progress

**Code repos (source of truth for architecture):**

| Repo | README |
|---|---|
| Next.js storefront | [midbec-front](../midbec-front/README.md) |
| Go API | [midbec-go-api](../midbec-go-api/README.md) |

UnoPIM integration details: [`midbec-go-api/docs/unopim-catalogue.md`](../midbec-go-api/docs/unopim-catalogue.md)

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
| 9 | Unified header search — autocomplete + `/recherche` page (part mode) | ✅ Done |
| 10 | UnoPIM — OAuth2 auth, category cache, Go proxy | ✅ Done |
| 11 | UnoPIM — category tree, icons, dynamic catalogue menu | ✅ Done |
| 12 | UnoPIM — product listing + unified navigation + drill-down panel | ✅ Done |
| 13 | UnoPIM — header search (ERP discovery + PIM enrichment) | ✅ Done |
| 14 | Interim ERP catalog + product detail page E2E + shop cleanup Phase 1 | ✅ Done |
| 15 | ERP catalog UX polish (title-case, leaf megamenu) + minimal CI/CD | ✅ Done (Jun 19) |
| 16 | B2B checkout — live ERP calculate + cart totals display | ✅ Done (Aug 4) |
| 17 | Checkout guest guardrails — no phantom anonymous order path | ✅ Done (Aug 5) |
| 18 | Order confirmation — server-backed `GET /api/orders/{orderNo}` | ✅ Done (Aug 11) |
| 19 | Pre-submit calculate parity — displayed total matches ERP create | ✅ Done (Aug 11) |
| 20 | Invoices pipeline — list + download API | 🟡 Shipped Jul (UI + API) — `/test` E2E probe blocked |
| 21 | Front hygiene — quickview removal, megamenu i18n, audit triage | ✅ Done (Aug 12–13) |
| 22 | Homepage → ERP carousels + static checkout countries | ✅ Done (Aug 13) — legacy homepage audit pending |

> **Active catalog:** ERP (`NEXT_PUBLIC_CATALOG_SOURCE=erp`). UnoPIM remains the long-term product source of truth — blocked pending infra/import (Patrick).

> **Active phase (Aug 2026):** checkout/payment hardening + strangler cleanup of fake template APIs. Full fake-server removal waits until homepage and checkout no longer depend on legacy helpers.

---

## 🛠️ Stack

Full details in [`stack.md`](./01%20-%20Context/stack.md) — revalidate against code READMEs after major changes.

| Layer | Tech |
|---|---|
| Frontend | Next.js 15 · React 19 · TypeScript 5.8 · Tailwind CSS v4 |
| Frontend state | Redux Toolkit (8 slices) · TanStack Query v5 · Zustand migration planned |
| Backend | Go 1.25 · Chi · PostgreSQL (pgx, raw SQL) |
| Backend pattern | Handlers → ERP/PIM clients → repositories (no service layer) |
| PIM | UnoPIM (long-term product source of truth) |
| ERP | Ogasys via Go API (active catalog + orders + pricing) |
| i18n | next-intl (routing) + react-intl (UI strings) — FR / EN |
| Infra | LXC containers · GitLab CI/CD (Patrick) |
| Package manager | Bun (front) · Go modules (back) |

---

## 🧠 The approach

Each daily log follows a consistent format (see [`.cursorrules`](./.cursorrules)):

- **Humeur & contexte** — a human note on the day
- **Objectifs** — what was planned
- **Découverte du jour** — one insight, tool, or observation
- **Réalisations** — what was actually done, with enough detail to reconstruct the reasoning
- **Ce que j'ai appris** — one generalizable principle
- **Validation** — manual checks when relevant (optional)
- **Vigilance** — traps, gotchas, things to watch
- **Next steps** — what's queued
- **Énergie** — one sentence on the day's state

Principles that show up repeatedly across the logs:

- **Audit before touching anything** — read/grep before every change
- **One scope = one commit** — Ryan executes Git manually; agents propose, human validates
- **Strangler fig over big bang** — migrate domain by domain, never all at once
- **Client is not source of truth** — especially for money, orders, and persisted state
- **Docs have an expiry date** — revalidate architecture notes against code (learned Aug 11)
- **YAGNI enforced** — features built on confirmed need, not speculation

---

## 📝 Notes

- Logs are written in **French** (my working language at Midbec)
- This repo is a signal of *engineering approach*, not a technical specification
- **No Trello ticket numbers** in daily logs — plain language for a public audience
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
