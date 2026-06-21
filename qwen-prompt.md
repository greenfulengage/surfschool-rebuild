# Qwen 2.5 build prompt — Scarborough Beach Surf School homepage

This file has three parts:
1. **How to run it** on the Mac Mini (for you, Rob)
2. **THE PROMPT** — copy everything inside the fenced block into Qwen
3. **What to check** in the output to judge how well Qwen did

---

## 1. How to run it on the Mac Mini

- **Model:** use a *Coder* variant — `qwen2.5-coder:32b` if you have the RAM (≈24 GB+), else `qwen2.5-coder:14b`, or `:7b` as a fast/low‑RAM fallback. The Coder models are much better at clean HTML/CSS than the general `qwen2.5` chat models.
- **Runtime:** Ollama (`ollama run qwen2.5-coder:14b`) or LM Studio both work.
- **Settings:** temperature **0.2–0.3** (you want correctness, not creativity), and make sure the context window is large enough for this long prompt — set `num_ctx` to **8192** or higher in Ollama.
- **One-shot:** paste the whole prompt block as a single message. The output should be one complete `index.html` file — save it as `index.html` and open it in a browser.
- This is a deliberately *self-contained* prompt: it contains all the business facts, image URLs, prices, the real TuriTop booking embed and the colour palette, so Qwen doesn't have to invent anything or go online.

---

## 2. THE PROMPT  (copy everything between the lines below)

```
You are an expert front-end web developer. Produce a single, complete, production-ready static HTML file (index.html) for a surf school's homepage. Output ONLY the code — one file, starting with <!DOCTYPE html> and ending with </html>. No explanation before or after.

GOAL
A fast, modern, accessible, mobile-first marketing homepage that replaces an old, slow WordPress site. It must feel contemporary and load almost instantly. Plain HTML + CSS only. No build tools, no frameworks, no external JavaScript except the two things explicitly listed below (Google Fonts and the TuriTop booking widget). Put all CSS in a single <style> block in the <head>.

THE BUSINESS (use these facts exactly — do not invent details)
- Name: Scarborough Beach Surf School
- Tagline: Perth's top-rated, family-run surf school. "The world's oldest surf school", teaching since 1986.
- Location: The Esplanade, Scarborough, Perth, Western Australia 6019
- Phone: 0416 589 141 (international +61 416 589 141) — make it a tap-to-call tel: link
- Email: surf@surfschool.com
- Reviews to show as trust signals: 5.0 stars from 512 Google reviews; 4.9 stars from 195 Tripadvisor reviews
- Social links: Facebook https://www.facebook.com/perth.surfschool/ , Instagram https://www.instagram.com/scarboroughbeachsurfschool/ , YouTube https://www.youtube.com/channel/UCIV-VhNvyeaSX0xKNbsKCjA
- Language/locale: Australian English (en-AU)

LESSONS TO FEATURE (as a responsive grid of cards — title, location, 1-2 sentence description, price, "Read more" link href="#book")
1. "2.25 Hour Surf Lesson" — Scarborough Beach — Flagship lesson for beginners and intermediates; early sessions for the best waves and no crowds. — $79 per person — tag: "Most popular"
2. "Level 1 Beginner Course" — Scarborough Beach — 2 to 5 lesson courses; skills improve fast; from $59 per lesson; up to 12 months to complete. — From $150 — tag: "Best value"
3. "Level 2 Intermediate" — Scarborough Beach — Small groups mean more waves; learn to read waves and surf both left and right. — From $79 per person
4. "Leighton Beach Lesson" — Leighton Beach — 2.25 hour winter lessons with a warm 4mm full-length wetsuit; beginners and intermediates. — $79 per person — tag: "Winter season"
5. "School Holiday Courses" — Teens 13+ — Popular holiday programs for teenagers; teaching surfing since 1986. — From $79 per person
6. "Private Group Lessons" — Ages 10 and older — Just your family and friends with your own dedicated coach; great for celebrations and corporate groups. — Enquire (private rate)

PRICING FACTS (for schema and any pricing text): single 2.25hr lesson $79; 2-lesson course $150; 3-lesson $210; 4-lesson $260; 5-lesson $295. All lessons include surfboards and O'Neill wetsuits. Group sizes are small: 4 to 6 students per lesson.

IMAGES (use these exact URLs as <img> src; every image MUST have descriptive alt text)
- Hero background: https://www.surfschool.com/wp-content/uploads/2024/10/hayata-4.scarborough.jpg.webp
- Card 1 (2.25hr): https://www.surfschool.com/wp-content/uploads/2024/11/mylene-scarborough-2.25-hours.jpg.webp
- Card 2 (Level 1): https://www.surfschool.com/wp-content/uploads/2024/04/scarb-2.25.jpg.webp
- Card 3 (Level 2): https://www.surfschool.com/wp-content/uploads/2024/02/Intermediate-surfer.jpg
- Card 4 (Leighton): https://www.surfschool.com/wp-content/uploads/2024/10/ruby-surfing-scarboorugh-e1728542714898.jpg
- Card 5 (School Holiday): https://www.surfschool.com/wp-content/uploads/2025/10/school-holiday-classes.jpg
- Card 6 (Private): https://www.surfschool.com/wp-content/uploads/2025/10/sisi-lolo-private-group.jpg.webp
- "Why us" section photo: https://www.surfschool.com/wp-content/uploads/2024/02/teen-lessons.jpg

PAGE SECTIONS (in this order)
1. Sticky header: brand name on the left, anchor nav (Lessons, Why us, FAQ, Book), and a prominent "Book a lesson" button linking to #book. Collapse nav sensibly on mobile.
2. Hero: full-width background image (the hero URL above) with a dark gradient overlay for text contrast; an eyebrow line ("Perth's top-rated · family-run since 1986"); an H1 ("Catch your first wave at Scarborough Beach"); a short lead paragraph; two buttons ("Book online 24/7" → #book, "See all lessons" → #lessons); and a small stat row ("4–6 surfers per group", "2.25 hrs in the water", "All gear included").
3. Trust strip: a horizontal bar of ticked points — Accredited surf coaches · Small group & private lessons · All equipment provided · Free easy parking · 5.0★ from 512 Google reviews.
4. Lessons: section heading + the responsive 6-card grid described above.
5. Why us: two-column split — left = heading "Long lessons, with coaches who care" and 3 short feature points (small groups of 4–6; early sessions beat the crowds and the seabreeze, free parking; top gear — B Softboards and O'Neill wetsuits); right = the "Why us" photo.
6. Book (id="book"): a strong call-to-action section with the TuriTop booking widget embedded (see below) and a line "Secure payment · gift vouchers available · 24-hour cancellation".
7. FAQ (id="faq"): an accordion or simple list using the 4 Q&As below.
8. Footer: address (NAP exactly as above), tap-to-call phone, email link, social links, "Established 1986", and a current-year copyright.

FAQ CONTENT (use verbatim; also mirror in FAQPage schema)
Q: What do I need to bring? A: Wear your bathers, and bring a small bag for your clothes and a towel. We provide top-of-the-range O'Neill wetsuits and B Softboards, and lock your bag away while you surf.
Q: What's the difference between the 2.25 hour and 1.5 hour lesson? A: The 2.25 hour premium lesson ($79) gives you more time in the water and is run at the best early time slot for beginners and intermediates. The 1.5 hour lesson is a shorter beginner "give it a go" session.
Q: Should I book a Level 1 or Level 2 course? A: If you can already pop to your feet cleanly in one motion on small green waves, you're ready for Level 2. If you're unsure, book Level 1 and we'll assess you in the first lesson.
Q: Do course lessons have to be on consecutive days? A: No — the days are your choice and don't have to be consecutive. You have up to 12 months to complete a course.

BOOKING WIDGET (paste these two snippets exactly — do not modify the IDs)
Put this <div> inside the Book section where the calendar should appear:
<div class="load-turitop" data-service="P32" data-lang="en" data-embed="box"></div>
And put this <script> just before </body>:
<script src="https://app.turitop.com/js/load-turitop.min.js" data-company="S559" data-buttoncolor="green" data-ga="no"></script>

DESIGN DIRECTION
- Fonts: load from Google Fonts — "Archivo" (700/900) for headings, "Inter" (400/500/600) for body.
- Colour palette (CSS variables): ink #0c1f2c, sea #0a7ea4, sea-deep #075f7d, sun #ffc83d, sand #f6f1e7, white #ffffff.
- Modern feel: generous spacing, rounded corners (~16px) on cards, soft shadows, a subtle hover lift on cards, smooth scroll for anchor links. Buttons are pill-shaped. Keep it clean and uncluttered — not "templated".
- Fully responsive: 3-column card grid on desktop, 2 on tablet, 1 on mobile; hero text must stay readable on small screens.

TECHNICAL REQUIREMENTS (important for search engines and AI assistants)
- Correct <head>: <meta charset>, responsive viewport, a keyword-rich <title> ("Surf Lessons in Perth | Scarborough Beach Surf School"), a meta description, Open Graph tags, and lang="en-AU" on <html>.
- Semantic HTML5 (header, nav, main, section, article, footer) with ONE <h1> and a sensible heading hierarchy.
- Accessibility: descriptive alt text on every image, aria-labels on icon-only links, sufficient colour contrast, keyboard-focusable interactive elements.
- Add JSON-LD structured data in <script type="application/ld+json"> blocks:
  (a) a "SportsActivityLocation" (or LocalBusiness) object with name, address, telephone, url, priceRange, and an aggregateRating of ratingValue 5.0 / reviewCount 512;
  (b) a "FAQPage" object containing the 4 Q&As above.
- No layout-shift hacks; images should have width/height or aspect-ratio styling so the page doesn't jump.
- The whole page must be a single self-contained file that works by simply opening index.html in a browser.

Now output the complete index.html.
```

---

## 3. What to check in Qwen's output (quick scorecard)

Open the generated `index.html` in a browser and rate it:

- **Renders cleanly?** Header, hero, 6 lesson cards, why-us, book, FAQ, footer all present and laid out, not broken.
- **Booking widget loads?** The TuriTop calendar/button appears in the Book section (it needs internet; the two snippets must be unmodified — `data-company="S559"`, `data-service="P32"`).
- **Images load?** All 8 photos appear (they're hot-linked from the live site).
- **Responsive?** Resize the window — cards reflow 3→2→1, hero stays readable.
- **Schema present?** View source and confirm the two JSON-LD blocks (LocalBusiness + FAQPage) are there and valid — paste into Google's Rich Results Test to be sure.
- **Accessibility basics?** Every `<img>` has real alt text; there's exactly one `<h1>`; phone is a `tel:` link.
- **Speed/cleanliness?** One file, no frameworks, CSS in one `<style>` block, no leftover placeholder text.

If a 14B/32B Coder model nails most of this in one shot on the Mac Mini, that's a strong signal Craig could have a fully **locally-built, self-owned** site — which directly answers his "proprietary control / understand it myself" goal. If the smaller models stumble on the schema or responsiveness, that tells you where a frontier model (or a human pass) still earns its keep.
