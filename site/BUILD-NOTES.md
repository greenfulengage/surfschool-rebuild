# Scarborough Beach Surf School — full static site build

Fast, hand-coded static site. No WordPress, no database, no build step. Serves as-is on
GitHub Pages, Cloudflare Pages or Netlify.

## Pages (16)
- `/` homepage — hero, lessons, why-us, reviews, about teaser, LocalBusiness+AggregateRating schema
- `/lessons/` index — all 6 lessons + single-source price table
- `/lessons/scarborough-225/` flagship 2.25hr (Product schema, TuriTop booking)
- `/lessons/leighton-beach/` winter
- `/lessons/level-1-course/`
- `/lessons/level-2-course/` (absorbs old /intermediate-surf-lessons/)
- `/lessons/school-holidays/` (absorbs old /teenagers-surf-lessons/)
- `/lessons/private/`
- `/faq/` — real 9 Qs + FAQPage schema
- `/about/` — story page (PLACEHOLDER team photos/story — needs Craig)
- `/surf-conditions/` — (PLACEHOLDER live surf widget spot)
- `/find-us/` — real Google map embed
- `/contact/`
- `/terms/`, `/privacy/` (noindex; starter copy — confirm with Craig)
- `/404.html`

## SEO / ranking protection
- Every lesson page has booking on-page (TuriTop S559 / P32) — the core conversion fix
- Schema: LocalBusiness+AggregateRating (home), Product+Offer (6 lessons), FAQPage (faq), Breadcrumb (all)
- Level 2 page is now indexable (old site had it noindexed)
- Single source of truth for prices + ages (was duplicated/conflicting across 5 pages)
- `sitemap.xml`, `robots.txt`, canonical tags on every page
- `_redirects` — 301 map from old WordPress URLs (Netlify/Cloudflare format)

## BEFORE GO-LIVE — still needed from Craig
1. Real Google review quotes (homepage has 3 placeholders written in-voice)
2. About page: real team photos + founder story (marked placeholder)
3. Surf conditions: live widget (marked placeholder)
4. Confirm blog retirement (currently /blog/ → /surf-conditions/)
5. Confirm terms + privacy wording
6. Verify full URL list vs https://www.surfschool.com/sitemap_index.xml
7. Baseline Search Console metrics + Core Web Vitals BEFORE switching DNS

## Notes
- Photos hotlink from the existing surfschool.com CDN — fine for preview; host them
  properly (or migrate the media) before final cut-over.
- Kids-under-13: built 13+ throughout. Adding a /lessons/kids/ page later is an SEO
  opportunity (a competitor owns that search) — flagged for Craig.
