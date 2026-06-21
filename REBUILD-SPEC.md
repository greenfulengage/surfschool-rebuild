# Scarborough Beach Surf School — Website Rebuild Scope

**Current site:** https://www.surfschool.com/ (WordPress)
**Goal:** Replace WordPress with a fast, modern, low-maintenance site that doesn't look "word-pressy" — keeping the existing booking flow intact.
**Date:** 15 June 2026

---

## TL;DR

This is a small brochure site (~16 pages) with one dynamic dependency: bookings. The booking and payment system is **TuriTop**, a third-party embedded widget that has nothing to do with WordPress and can be dropped into any HTML page with two lines of code. That means the whole site can be rebuilt as a fast static site with **zero risk to bookings or payments**.

**Effort:** Roughly 2–4 days for a full static rebuild of all pages with a facelift. A homepage-only facelift is a half-day. No database, no logins, no server code.

---

## What the current site runs on

| Layer | Current | Notes |
|---|---|---|
| CMS | WordPress | The thing you want to leave |
| Page builder | WPBakery (`js_composer`) | Heavy, bloated markup — the main source of "word-pressy" feel |
| Caching | WP Rocket 3.22 | Already installed to paper over WP's slowness |
| Images | WebP + lazyload | Already optimised; can be reused as-is |
| Bookings + payments | **TuriTop** (company `S559`) | External widget — fully portable |
| Maps | Google Maps embed | Standard iframe, portable |
| Video | YouTube embeds | Portable |
| Fonts | Google Roboto | Portable |

The only "real" software here is WordPress + WPBakery. Everything else is an embed that travels to a new site untouched.

---

## The booking system (the one thing that matters)

Everything on the site funnels to **"Book Online 24/7."** That flow is powered entirely by TuriTop:

```html
<!-- Loader (once per page) -->
<script src="https://app.turitop.com/js/load-turitop.min.js"
        data-company="S559" data-buttoncolor="green"></script>

<!-- Booking widget (anywhere you want a calendar / button) -->
<div class="load-turitop" data-service="P32" data-lang="en" data-embed="box"></div>
```

Implications for the rebuild:
- **No migration needed.** The same snippet works on a static HTML page, Astro, Eleventy, Squarespace — anything.
- **Payments, gift vouchers, multi-lesson courses, confirmation emails, the "book later" links** described in the FAQ are all handled inside TuriTop. None of that is WordPress.
- Each lesson type is a TuriTop "service" (e.g. `P32`). The rebuild just needs the correct service ID per lesson page.
- **This removes the only thing that would normally make a surf-school rebuild risky.**

---

## Full page map (16 pages)

All pages share the same template: header/nav → hero image → text + image blocks → Google Map → footer. Rebuilding the template once covers every page.

### Core
1. **Home** — hero, intro, trust ticks, grid of 7 lesson cards, map, footer
2. **FAQ** — 9 Q&A accordion (gift vouchers, lesson lengths, course pricing, booking flow, what to bring, etc.)

### Lessons (the money pages — each has a TuriTop widget)
3. **Book Prepaid Vouchers** — booking calendar landing page *(noindex)*
4. **Surf Lessons Scarborough 2.25hr** — flagship product + price list
5. **Level 1 Surf Course** — beginner multi-lesson course
6. **Level 2 Surf Course** — intermediate course
7. **Teenagers Surf Lessons**
8. **School Holiday Surf Lessons** — teens 13+
9. **Leighton Beach Surf Lesson** — winter-season location
10. **Private Surf Lessons** — private groups, 10yrs+

### Surf Tips (blog / SEO content)
11. **Blog index**
12. **About Surfing Tips**
13. **Surfing Equipment Tips**
14. **Surf Conditions**
15. **Intermediate Surf Lessons**

### Contact / legal
16. **Contact**, **Find Us**, **Terms & Conditions**, **Privacy Policy**

> Note: the FAQ also references a **1.5hr "Give it a go" lesson** page (`/give-it-a-go-surf-lesson/`) not in the current nav — worth confirming whether it should be kept.

---

## Pricing reference (currently hardcoded in page copy)

| Product | Price | Per lesson |
|---|---|---|
| 1 × 2.25hr lesson | $79 | $79 |
| 2-lesson course | $150 | $75 |
| 3-lesson course | $210 | $70 |
| 4-lesson course | $260 | $65 |
| 5-lesson course | $295 | $59 |
| 1.5hr "Give it a go" | $55 | — |

Courses valid 12 months; 24hr cancellation notice. (Prices also live inside TuriTop — keep the two in sync, or better, link out and stop hardcoding them in copy.)

---

## Content to keep vs. cut

**Keep:**
- All lesson page copy and the real photos (already WebP-optimised on their CDN — reusable)
- FAQ content (good for SEO and reduces email load)
- Google Map, YouTube videos, social links, O'Neill / Surfing Australia trust badges
- The TuriTop booking embeds exactly as-is

**Worth a decision:**
- **Surf Tips blog** — thin but may carry SEO/local-search value. Recommend keeping the pages as static content (no live blog engine needed) unless analytics say they get no traffic.
- Twitter/X link (low value now)
- Inconsistent copyright years (2022/2024) and a duplicated footer — clean up in rebuild.

---

## Recommended approach

**Stack:** Static site — plain HTML/CSS, or a static generator (Astro or Eleventy) if you want reusable templates and easy content edits without touching code. No PHP, no database, no plugins to update or get hacked.

**Hosting:** Netlify, Cloudflare Pages, or similar — free/cheap, global CDN, near-instant loads, free SSL, auto-deploy.

**Why this kills the "word-pressy" feel:**
- WPBakery generates deeply nested, class-heavy markup; a hand-built template is a fraction of the size.
- Current pages ship ~1–2 MB and lean on WP Rocket to feel fast. A static page can be well under 200 KB and need no caching plugin.
- Full control over typography, spacing, and motion — the things that make a site feel custom rather than templated.

**Booking:** Paste the TuriTop snippet per lesson page. Done. No change to how customers book or pay.

**Effort estimate:**
- Homepage facelift only (proof of concept): ~½ day ✅ *(see attached POC)*
- Full static rebuild, all 16 pages, responsive, booking embeds wired in: ~2–4 days
- Optional: migrate to Astro/Eleventy with editable content templates: +1 day

**Risks:** Very low. The only integration (TuriTop) is copy-paste portable. Main task is rebuilding the layout and re-flowing existing content — not engineering.

---

## Open questions before a firm quote

1. **Keep the Surf Tips blog?** (SEO value vs. maintenance) — check analytics.
2. **Keep the 1.5hr "Give it a go" lesson** page that's missing from the nav?
3. **Who edits content** after launch — you (needs an editable CMS layer) or a developer (plain HTML is fine)?
4. **Domain/email/hosting** — staying where they are, or moving alongside the rebuild?
5. Confirm there's only **one TuriTop service per lesson**, and collect each service ID for the page embeds.
