<!-- created-by: claude-code -->
<!-- modified-by: claude-code -->
# CLAUDE.md — Syrixa organization

This file is the company-wide guide for Claude Code across all Nedex repos. Each product repo (Nedexedu, nedex-website, future products) has its own `CLAUDE.md` for product-specific rules; this one defines what is true everywhere.

## Identity

- Brand: **Syrixa**. Arabic-first SaaS company in the MENA region.
- Founders: Sami, Ahmad AS, Ahmad SU. Equal owners.
- Products live as separate repos under [`Syrixa-Sy`](https://github.com/Syrixa-Sy).

## Storage — cloud-only, nothing local

Everything Syrixa stores stays online. No product writes to a local disk for anything that needs to survive a request, a deploy, or a container restart.

- **Databases**: Supabase Postgres only. No SQLite, no local file-backed DBs, no embedded stores. Local dev points at a Supabase branch, not a local Postgres.
- **Files, uploads, generated assets**: Supabase Storage or Vercel Blob. Never the app's filesystem, never `/tmp` for anything that must outlive the request.
- **Caches & queues**: managed services (Upstash Redis, Supabase, Vercel KV). No on-disk caches.
- **Secrets & config**: Vercel/Supabase environment variables. No `.env` files committed; no secrets in source.
- **Logs & telemetry**: Vercel logs, Supabase logs, or a hosted provider. No log files written to disk.
- **Runtime**: Vercel Fluid Compute — assume the filesystem is read-only and ephemeral. Any code that does `fs.writeFile` to persist data is a bug.

If a feature seems to need local storage, the answer is to pick the right cloud primitive, not to write to disk.
