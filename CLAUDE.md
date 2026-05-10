<!-- created-by: claude-code -->
# CLAUDE.md — Nedex organization

This file is the **company-wide** guide for Claude Code across all Nedex repos. Each product repo (Nedexedu, nedex-website, future products) has its own `CLAUDE.md` for product-specific rules; this one defines what is true everywhere.

## Identity

- Brand: **Nedex**. Arabic-first SaaS company in the MENA region.
- Founders: Sami, Ahmad AS, Ahmad SU. Equal owners.
- Products live as separate repos under [`Nedex-Sy`](https://github.com/Nedex-Sy).

## Decision authority (applies across all repos)

| Area | Owner |
|---|---|
| DB schema, migrations, data integrity, auth, security, project board | Sami |
| Networking, infra, Vercel/Supabase, deployment, sales | Ahmad AS |
| UI, design system, frontend architecture | Ahmad SU |

**2-of-3 founder sign-off** is required for anything touching security, data loss, or money flows. No single owner ships those alone.

## Non-negotiable rules (org-wide)

1. **The document is the law. The code obeys.** Permission matrices, tier maps, and architecture docs are decided before code is written. If middleware and the matrix disagree, the code is wrong.
2. **Money flows are append-only.** No `UPDATE` on balances anywhere, in any product. Every transaction is a new immutable row + recompute.
3. **DB schema changes ship as Prisma migrations only.** Never "edit schema and push."
4. **Notion is the PM tool.** Tasks/Epics/Sprints live under the Nedexedu teamspace → **Project HQ**. Commits to `main` include `Closes MS-NN` referencing a Notion task; this auto-closes the task via workflow.
5. **Tag every AI-generated artifact.** First line: `<!-- created-by: skill-name -->`. If a different skill modifies it later, append `<!-- modified-by: skill-name -->`. Skill-owned folders are named `.skill-name/`.
6. **Do not read the `school-bracelet-archive` repo.** It is a deliberate hard-block (see Nedexedu rule 4). If a snippet is needed, a founder pastes it.

## Definition of Done (org-wide minimum)

A change is not done until:
1. Code merged to `main`.
2. Migrations applied to prod DB (if applicable).
3. One real user-flow tested by a human on the production URL.
4. Permission/role rows updated for every affected role (where applicable).
5. Repo docs updated (not Discord, not chat).
6. Notion task closed via `Closes MS-NN` in the commit message.

## Stack defaults (do not substitute without 2-of-3 sign-off)

| Layer | Choice |
|---|---|
| Web | Next.js 15 App Router (RSC) |
| Mobile | React Native + Expo (single TS codebase iOS+Android) |
| DB | Prisma + Supabase Postgres |
| Auth | JWT via `jose` — httpOnly cookies on web, bearer tokens on mobile, shared signing keys |
| UI | shadcn/ui + Tailwind, **Arabic RTL primary** |
| Hosting | Vercel (Fluid Compute) |
| Project config | `vercel.ts` (TypeScript-first) |
| Package manager | pnpm |

RTL is a primary requirement, not an afterthought.

## When this file disagrees with a product `CLAUDE.md`

Product-specific rules win **only if** they are stricter (more conservative) than the org rule, or cover a domain the org rule does not. They cannot relax org rules. If a product needs to relax an org rule, change this file first with 2-of-3 sign-off.
