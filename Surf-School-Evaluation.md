# Scarborough Beach Surf School — Website & Digital Presence Review

*An independent review of the current website, booking flow, search and AI visibility, and wider online presence — with the range of improvements available.*

Site reviewed: surfschool.com · June 2026

---

## At a glance

- The business is considerably stronger than its current website. Reputation is outstanding — **5.0 stars from 512 Google reviews** and **4.9 stars from 195 Tripadvisor reviews** — alongside genuine heritage as a surf school operating since **1986**.
- The site runs on **WordPress with the WPBakery page builder and a caching plugin**. This is the main reason it feels dated and loads slowly; most of the running cost is tied to keeping that stack going.
- **Bookings and payments run on TuriTop**, a third‑party system that is independent of WordPress. It can move to any new site unchanged, so a rebuild carries **no risk to bookings or payments**, and the existing booking dashboard stays exactly as it is.
- The booking calendar currently **loads only after a visitor interacts with the page**, and there is **no clear "Book" button on the individual lesson pages** — so the path from reading about a lesson to booking it is longer than it needs to be.
- One core lesson page (**Level 2**) is currently set to **"noindex,"** meaning it does not appear in Google at all.
- The exceptional review volume is **not reflected in search results**, because the site carries **no review, FAQ or product structured data**. This is the single largest untapped opportunity for both Google and AI‑answer visibility.
- Wider presence is **uneven**: Google and Tripadvisor are strong; social is fragmented (two Instagram handles, a dormant Twitter/X, a YouTube channel inactive for ~3 years); and there is **no presence on experience/gift marketplaces** — the channels best suited to passive, hands‑off bookings.
- A meaningful amount of **manual admin** sits behind each booking (copying into a daily run sheet, sending confirmation emails, sending day‑before reminders). Much of this can be **automated with an oversight step**.
- A **lean, modern static rebuild** would deliver near‑instant load times, a contemporary feel, full ownership of the code, and would reduce website‑specific running costs to roughly the price of a domain.
- **The opportunity spans more than the website** — it covers performance, search and AI visibility, reviews, booking‑workflow automation, and lead generation. Each is a distinct, measurable improvement.

---

## Summary

The underlying business is in good health; the website and surrounding digital setup are where the gap lies. A rare combination of assets — 38 years of heritage, a 5.0‑star Google rating across 512 reviews, and 4.9 stars across 195 Tripadvisor reviews — currently sits on a slow, dated WordPress site that hides its own booking button, removes one lesson page from Google, and relies on manual admin behind each booking.

The encouraging part is that the highest‑value fixes are also the lowest‑risk. The booking and payment system (TuriTop) is completely separate from WordPress, so it transfers to a new site untouched — the existing booking dashboard is unaffected. Most of what makes the site feel old and slow is the page‑builder and caching layer that exist only to run and prop up WordPress; removing them produces a far faster, cleaner site. And the most significant growth lever is not the website itself but the review reputation, which is currently invisible to search engines because the site lacks the structured data that would surface it.

Taken together, the work divides into clear streams — a modern rebuild, conversion improvements, technical SEO and structured data, review leverage, booking‑workflow automation, and lead generation — each of which stands on its own and adds measurable value.

---

## What the current site runs on

| Layer | Current | Observation |
|---|---|---|
| CMS | WordPress | The platform being replaced |
| Page builder | WPBakery (`js_composer`) | Main source of the heavy, "templated" feel |
| Caching | WP Rocket | Present to mask WordPress load times; also delays the booking calendar |
| Images | WebP + lazy‑load | Already optimised — reusable as‑is |
| SEO plugin | Yoast + Yoast Local | Local SEO partly configured (geo data present) |
| Bookings + payments | TuriTop (company `S559`) | External, fully portable — independent of the website |
| Hosting | SiteGround (Google Cloud, Sydney) | Managed WordPress hosting |
| Domain | Registered via Tucows | Registered 2003, renews Dec 2026 |
| Email | Google Workspace | Separate from hosting |

The only substantive "software" here is WordPress and the page builder. Everything else is an embed or service that moves to a new site unchanged. A hand‑built, lean site is a fraction of the page weight and fully under the owner's control.

---

## The booking system

Every page funnels to "Book Online 24/7," and that flow is handled entirely by TuriTop — a third‑party booking platform with no dependency on WordPress. The customer sees a colour‑coded availability calendar, a party‑size selector, the ability to add multiple dates for multi‑lesson courses, a gift‑voucher option, and secure online payment.

On the operator side, TuriTop already provides a bookings dashboard with full customer details, automatic acknowledgement emails to both operator and customer, scheduled reminders, payment handling, gift certificates, and staff logins. In other words, booking management already exists and would be retained.

Two points stand out as opportunities rather than faults:

- The booking calendar is delayed by the caching plugin and appears only after a visitor interacts with the page; on a lighter site it would load immediately.
- The lesson pages themselves describe each lesson and its price but carry no booking widget or clear "Book" button — the calendar lives only on a separate vouchers page. Surfacing booking on every lesson page would shorten the path to purchase.

A separate observation: comparable operators in the area use booking systems that add automated weather‑cancellation messaging and customer self‑rescheduling. TuriTop can also reduce manual steps through its reminders and confirmations; there is room to switch more of that automation on (covered under booking‑workflow automation below).

---

## Page‑by‑page health

The site is around 16 pages sharing a single template (header → hero → text/image blocks → map → footer).

| Page | In Google? | Booking prompt? | Notes |
|---|---|---|---|
| Home | Yes | Weak (text link) | Footer year out of date; no clear Book button near the top |
| Scarborough 2.25hr | Yes | No widget | Core page, prices shown, but no on‑page booking |
| Level 1 Course | Unclear | No | Missing meta tags |
| Level 2 Course | **No — set to noindex** | No | A core page currently invisible to Google |
| Teenagers | Yes | No | Age range reads "13–99" on a teens‑focused page |
| School Holiday | Yes | No | Minimum age inconsistent (11 vs 13) |
| Leighton Beach | Yes | No | Two H1 tags; "‑2" in the URL; framed winter‑only |
| Private Lessons | Yes | "Book 24/7" text, no link | A time typo; age 10 vs 13 elsewhere |
| FAQ | Yes | Links out | Strong content — but no FAQ structured data |
| Blog | Yes | No | Five posts; nothing added since 2022 |
| Surf Conditions | Yes | No | The richest content page on the site |
| Intermediate Lessons | Yes | No | A "blog post" performing a sales page's role; overlaps Level 2 |
| Contact | Yes | Form only | Footer duplicated; references a retired URL |
| Find Us | Yes | No | Minor typo; covers only one of two locations |
| Terms / Privacy | No (correct) | — | A few typos; otherwise appropriately hidden |

Recurring themes worth noting, all straightforward to resolve in a rebuild: no clear booking prompt on the lesson pages; one core page hidden from Google; an out‑of‑date footer year; a dormant blog; minimum age stated inconsistently across pages; prices duplicated across five pages; and a scatter of small typos and duplicated page elements.

---

## Strengths worth protecting

- **Reputation:** 5.0 stars from 512 Google reviews and 4.9 from 195 Tripadvisor reviews — a rare asset most operators in the category cannot match.
- **Heritage:** "the world's oldest surf school," operating since 1986 — defensible and memorable.
- **Value proposition:** long 2.25‑hour lessons in small groups of 4–6 — more time in the water per dollar than the common 1.5‑hour competitor format.
- **Location:** Scarborough, one of Perth's most visited beaches, with free parking.
- **Existing free listings:** present on Destination Perth (the regional tourism body) and displays recognised surf‑school accreditation.
- **Genuine content and photography:** the surf‑conditions and equipment pages, and the real lesson photos, are usable and worth carrying over.

---

## Search and AI visibility

The standout opportunity is that the review reputation is effectively invisible to search engines on the site today.

- **No review or rating structured data.** With 512 Google and 195 Tripadvisor reviews, adding rating markup can place star ratings beside the listing in search results — a well‑established way to lift click‑through.
- **No FAQ structured data**, despite a genuinely useful nine‑question FAQ — content that could earn additional space in both Google results and AI‑generated answers.
- **No product or price structured data** on the lesson pages, despite clear pricing.
- **One core lesson page set to noindex**, removing it from Google entirely.
- **Local search is only half‑built.** Geo data exists, but the Google Business Profile — the primary driver of "surf lessons near me / Perth" searches — is under‑leveraged and would benefit from photos, a booking link, and an ongoing review‑request habit.
- **Speed caps performance.** The page‑builder and caching stack limits mobile performance; a lean rebuild is the real fix.
- **AI‑answer visibility follows the same work.** Clean, fast, well‑structured pages with clear questions‑and‑answers and strong review signals are exactly what AI assistants draw on when recommending a business — so improving for Google and improving for AI are the same task.

---

## Online presence and where the business appears

| Channel | Present? | Active? | Notes |
|---|---|---|---|
| Own website | Yes | Partly | The booking hub, but dated and the Book prompt is hidden |
| Google Business Profile | Yes | Strong (5.0★, 512 reviews) | The best channel — and under‑optimised |
| Tripadvisor | Yes | Strong (4.9★, 195, #2 of 5 locally) | Excellent proof; not surfaced on the site |
| Destination Perth | Yes | Good | Free regional‑tourism listing |
| Facebook | Yes | Unclear | Listed as publisher; activity not publicly verifiable |
| Instagram | Yes — two handles | Weak | ~440 followers, split across two accounts |
| YouTube | Yes | Dormant | 72 subscribers, 8 videos, nothing in ~3 years |
| Twitter/X | Linked | Dormant | No recent activity |
| Experience/gift marketplaces | No | Gap | No presence on the channels best suited to passive bookings |

The reputation channels are doing the heavy lifting; social is fragmented; and the experience‑marketplace channels are entirely untapped.

---

## Competitor context

| Operator | Where | Beginner price | Booking system | Notes |
|---|---|---|---|---|
| Go Surf Perth | Same beach | $55 / 1.5hr | Viking Bookings | Polished site, accredited, automated weather messaging + self‑reschedule; also targets kids |
| Surfing WA Surf School | Trigg | from ~$130 private | Viking Bookings | Backed by the state body — high authority |
| Margaret River academies | Down south | $50–60 | Rezdy/FareHarbor‑style | Strong marketplace distribution — a useful model |

In context: pricing here is higher per ticket ($79 vs $55) but lower per hour ($35 vs $37), with smaller groups and ~50% more time in the water — a strong value story that is currently understated. Competitors' main edges are booking automation and marketplace reach, both of which are addressable, while reviews and heritage already lead on trust.

---

## Opportunities — the scope of what can be improved

The work divides into distinct streams. Each delivers value independently; together they compound.

**1. A modern, lean rebuild.** Replace WordPress and the page builder with a fast static site — near‑instant load, a contemporary feel, and full ownership of the code on portable, non‑proprietary foundations. Hosting moves to a free/near‑free tier, cutting most current running costs.

**2. Conversion improvements.** A clear "Book" prompt on every lesson page, a booking calendar that loads instantly, and a sharper articulation of the value proposition (2.25‑hour lessons, small groups, since 1986, 500+ five‑star reviews) — turning more of the existing traffic into bookings.

**3. Technical SEO and structured data.** Review/rating, FAQ and product markup so search results can show star ratings and richer listings; correcting the noindex page; a complete sitemap; clean headings and metadata. This is also what positions the business well in AI‑generated recommendations.

**4. Review leverage.** Optimising the Google Business Profile and introducing a simple, near‑automatic review request after each lesson — compounding an already category‑leading reputation and feeding it back into search ranking.

**5. Booking‑workflow automation.** Reducing the manual admin behind each booking: automatically updating the daily run sheet from incoming bookings (with a review/edit step), preparing the detailed confirmation emails (including course progress) for quick approval, and automating the day‑before reminders — each with an oversight option. This directly reduces time spent at the computer.

**6. Lead generation.** Listing on experience/gift marketplaces for passive, commission‑based bookings; making gift vouchers prominent; and capturing not‑ready‑yet visitors (e.g. a simple surf‑conditions email sign‑up) so tourist and gift‑buyer demand isn't lost.

**7. Content and housekeeping.** Consolidating overlapping pages, retiring the dormant blog into evergreen content, standardising pricing and age information to a single source, and clearing small inconsistencies — a cleaner, more trustworthy site.

**8. Social consolidation.** Resolving the duplicate Instagram handle, pointing all links to one account, and repurposing existing video — a tidier, more credible social footprint with little ongoing effort.

---

## Indicative effort and running cost

| Item | Now (approx/yr) | After a rebuild |
|---|---|---|
| Hosting | ~$215–360 | ~$0 (static hosting free tier) |
| Caching plugin | $59 | $0 (not required) |
| Page builder | one‑time, ~$0 ongoing | $0 |
| Booking system (TuriTop) | ~$370+ | ~$370+ (retained) |
| Domain | ~$20 | ~$20 |
| Email (Google Workspace) | ~$84 (if paid) | ~$84 |
| **Website‑specific running cost** | **~$300–400/yr** | **≈ $20/yr** |

Most current spend is tied to the WordPress stack. After a rebuild, the only meaningful ongoing website cost is the booking system, which applies on any platform.

Indicative build effort: a homepage facelift is roughly half a day (already prototyped); a full static rebuild of all pages with booking embeds, structured data and redirects is in the order of a few days; a simple self‑edit layer adds about a day; and the lead‑generation and automation work runs partly as ongoing activity. Risk throughout is low, as the only external dependency (TuriTop) is fully portable.

---

## Open considerations

- **Self‑editing:** a simple, friendly editor for occasional changes, versus changes being handled on the operator's behalf — the lower‑effort option suits a preference for less time at the computer.
- **Booking system:** retaining TuriTop (lowest‑risk, familiar) and switching on more of its automation, with any change of engine treated as a separate, later decision.
- **Kids under 13:** whether to add an offering and page for the under‑13 segment, which a nearby competitor currently owns, or remain 13+.
- **Blog:** retiring it and folding any useful content into permanent pages.
- **Marketplaces:** willingness to list on experience/gift platforms for passive, commission‑based leads.
- **Email, hosting and domain:** retaining email and the domain as they are, and moving only the website hosting.
- **Sequencing:** launching the rebuilt site first, then layering the lead‑generation and automation work, or running them together.

---

## Appendix

**Confirmed facts.** Booking/payments: TuriTop (company `S559`, service `P32`), an embeddable widget with no WordPress dependency. Hosting: SiteGround on Google Cloud (Sydney). Domain registrar: Tucows, registered 2003, renews Dec 2026. Email: Google Workspace. Reviews: Google 5.0★ / 512; Tripadvisor 4.9★ / 195 (#2 of 5 locally). YouTube: 72 subscribers, 8 videos, newest ~3 years old. Sitemap present at `/sitemap_index.xml`; robots file omits the sitemap reference.

**Pricing on the current site.** Single 2.25hr lesson $79; 2‑day course $150; 3‑day $210; 4‑day $260; 5‑day $295 (valid 12 months; 24‑hour cancellation). 1.5hr "give it a go" $55. Private: 1 surfer $145 up to 8 surfers $440.

**Sources.** Live site (all lesson, FAQ, contact, booking and legal pages); TuriTop features and pricing; Tripadvisor listing; Go Surf Perth, Surfing WA Surf School and Margaret River academy sites; Destination Perth listing; published hosting and plugin pricing.
