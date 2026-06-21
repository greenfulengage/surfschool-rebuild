# Surf School Rebuild — Project Handoff & Context

**Purpose:** Paste this into a new Claude chat to continue the surfschool.com rebuild with full context. A previous session did the research, wrote the evaluation, built a homepage prototype, and published everything to GitHub. This document carries that over so the new chat can pick up without repeating the work.

---

## How to start the new chat

Make sure the **GitHub connector is enabled**, then send something like:

> "I'm continuing a website rebuild project. First, read my GitHub repo **https://github.com/greenfulengage/surfschool-rebuild** to see what's been done so far, then use the context below. We're building the new site with you (Claude). Don't worry about the local-LLM/Qwen idea — we've dropped it."

*(Confirm that repo URL — replace `greenfulengage`/`surfschool-rebuild` if your username or repo name differs. Live site: https://greenfulengage.github.io/surfschool-rebuild/ , evaluation: add `/evaluation/`.)*

---

## What's in the repo (current state)

- `index.html` — a fast, modern **static homepage prototype** (the agreed direction). Uses the real TuriTop booking widget.
- `evaluation/index.html` + `Surf-School-Evaluation.md` / `.docx` — the **client-facing evaluation** (neutral tone, no names) covering findings, SEO/AI visibility, presence, competitors, and an 8-stream opportunity list. This is the scoping/sales document.
- `REBUILD-SPEC.md` — short technical scope note.
- `README.md` — repo overview + publish instructions.
- `CARRYOVER-bundle.md` — all files concatenated (ignore; just a transit copy).

**First action for the new chat: read the repo, especially `index.html` and `Surf-School-Evaluation.md`.**

---

## Who's who

- **Craig** — owner of **Scarborough Beach Surf School** (surfschool.com), Perth WA. Older, not a tech person, wants: *less time on the computer, more leads, a site he can understand and modify, full ownership/proprietary control (no lock-in like the old site), a contemporary feel, and to keep his existing booking system.*
- **Rob / Webposty** — the builder (the person you're talking to). Building the new site **with Claude**.

---

## The business — key facts

- surfschool.com, Scarborough/Leighton beaches, Perth WA. Trading since **1986** ("world's oldest surf school"). Family-run.
- Reputation (its biggest asset): **Google 5.0★ / 512 reviews**, **Tripadvisor 4.9★ / 195** (#2 of 5 locally).
- Current stack: **WordPress + WPBakery page builder + WP Rocket** caching; **SiteGround** hosting (Google Cloud Sydney); domain via **Tucows** (renews Dec 2026); email on **Google Workspace**.
- **Bookings + payments: TuriTop** — company `S559`, service `P32`. It's a portable JS embed, independent of WordPress. **KEEP IT** in the rebuild (the two embed lines are in `index.html`). Customers get a calendar + payment; the owner already has a TuriTop dashboard with bookings, confirmations, reminders, gift vouchers.
- Lesson pricing: single 2.25hr $79; courses 2=$150, 3=$210, 4=$260, 5=$295; private 1=$145 → 8=$440. Small groups (4–6). Mostly 13+, private 10+.

---

## What the review found (brief)

Slow, dated WordPress site; **no clear "Book" button on the lesson pages** and the booking calendar only loads after interaction; the **Level 2 page is set to noindex** (invisible to Google); **no review/FAQ/product schema**, so the excellent reviews are invisible to search and AI; dormant blog; fragmented social (two Instagram handles, dormant Twitter/X, YouTube inactive ~3 years); **no presence on experience/gift marketplaces**; and a lot of **manual admin** behind each booking.

---

## Direction agreed

- **Lean static rebuild** (plain HTML or Astro) — fast, modern, fully owned/portable, no proprietary lock-in. Build it **with Claude**.
- **Hosting:** currently GitHub Pages (as a live preview/share); could move to Cloudflare Pages/Netlify or the real domain later.
- **Keep TuriTop** unchanged.
- **Evaluation stays neutral** (no names, observational) — it's used to scope/sell the work.

---

## The opportunity / scope (the value stack — 8 streams)

1. **Modern lean rebuild** — speed, contemporary feel, ownership, near-zero hosting cost.
2. **Conversion** — a clear "Book" button on every lesson page; calendar loads instantly; sharpen the value story (2.25hr, small groups, since 1986, 500+ 5★).
3. **Technical SEO + structured data** — LocalBusiness/AggregateRating, FAQPage, Offer/Product schema; fix the noindex page; clean sitemap/metadata. Also drives AI-answer visibility.
4. **Review leverage** — optimise Google Business Profile + a simple post-lesson review-request.
5. **Booking-workflow automation** — see next section.
6. **Lead generation** — experience/gift marketplaces; prominent gift vouchers; email capture.
7. **Content & housekeeping** — consolidate overlapping pages, retire the blog, single source for prices/ages, fix inconsistencies.
8. **Social consolidation** — one Instagram handle, repurpose video.

---

## Booking back-end automation goals (from Craig)

Today, after a TuriTop booking: TuriTop auto-acknowledges the customer, then Craig manually copies it into a **"run sheet"** (daily roster + per-student history + course progress), sends a **detailed confirmation email** (lessons booked/remaining for courses), and sends **day-before reminders**. He wants these automated **with an oversight/approval step**:

- Auto-populate the run sheet from new bookings (review/edit).
- Auto-prepare confirmation emails (with course progress) — draft-for-approval first, then optionally auto-send.
- Auto-send day-before reminders off the run sheet (with oversight).

**Recommended approach:** keep TuriTop as source of truth; layer a **Google Sheet "run sheet"** + automation (Make/Zapier, or TuriTop's API/webhooks); confirmations land as Gmail drafts for one-click send initially. **Still to verify:** TuriTop's exact API/webhook/Zapier support and native reminder/course-tracking capabilities — do this before promising specific wiring. This is a workstream parallel to the website.

---

## Open decisions (not yet settled)

- Self-edit: a simple friendly editor vs. agency-managed updates (his "less computer time" goal leans agency-managed).
- Add a **kids under 13** offering/page (a competitor owns that search), or stay 13+?
- Retire the blog (fold useful content into evergreen pages)?
- List on experience/gift marketplaces (commission-based)?
- Keep email/domain as-is, move only website hosting?
- Launch the rebuilt site first, then layer lead-gen/automation — or together?

---

## Suggested next steps for the new chat

1. **Read the repo** to see the homepage prototype and evaluation.
2. **Build the full multi-page static site** from the prototype: all ~16 pages, responsive, a **Book button + TuriTop on every lesson page**, plus the JSON-LD schema (LocalBusiness/AggregateRating, FAQPage, Offer) and clean meta/sitemap. Keep the TuriTop embed exactly (`data-company="S559"`, `data-service="P32"`).
3. **Set up 301 redirects** mapping the old WordPress URLs to the new pages so search rankings carry over.
4. **Verify TuriTop's API/automation**, then spec the run-sheet/confirmation/reminder automation.
5. Keep the **evaluation document in sync** as scope firms up.

**Guardrails:** keep it static, portable, and owned by Craig (no proprietary lock-in); keep TuriTop; keep client-facing copy neutral and professional.
