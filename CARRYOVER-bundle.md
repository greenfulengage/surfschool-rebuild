# Scarborough Beach Surf School — full project bundle

Everything for the surfschool.com rebuild in one file: homepage prototype, the neutral evaluation, the rebuild scope, the Qwen build prompt, and the repo README. Each file is delimited by a clear marker so it can be split back out (or handed to a GitHub-connected assistant with: "create each of these as a file in my repo and commit").

Generated: 2026-06-21 04:27 UTC


================================================================
===== FILE: README.md
================================================================

# Scarborough Beach Surf School — rebuild working repo

Working files for the surfschool.com rebuild: a fast static homepage prototype, the full website evaluation (as a live page + Word doc), the rebuild scope, and the local-LLM build prompt.

## What's in here

| File / folder | What it is | Live URL (once Pages is on) |
|---|---|---|
| `index.html` | Fast static homepage prototype (keeps the real TuriTop booking widget) | `https://USERNAME.github.io/REPO/` |
| `evaluation/index.html` | The full evaluation & rebuild scope, rendered as a styled web page | `https://USERNAME.github.io/REPO/evaluation/` |
| `Surf-School-Evaluation.docx` | Same evaluation as a Word document (for printing / the meeting) | downloadable from the repo |
| `Surf-School-Evaluation.md` | Evaluation in Markdown (renders in the GitHub repo view) | — |
| `REBUILD-SPEC.md` | Short technical scope note | — |
| `qwen-prompt.md` | Self-contained prompt to rebuild the homepage on a local model (Qwen 2.5) | — |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is (no Jekyll processing) | — |

> Replace `USERNAME` and `REPO` above with your GitHub username and repository name.

## Publish it (one-time, ~2 minutes)

From this folder, in Terminal:

```bash
git init
git add .
git commit -m "Surf school rebuild: homepage prototype + evaluation"
git branch -M main
git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

Then turn on GitHub Pages (this is a settings click only you can make):

1. On GitHub, open the repo → **Settings** → **Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/(root)**. Save.
4. Wait ~1 minute, then your live URLs above will work.

## Pushing changes from now on

Edit any file, then:

```bash
git add .
git commit -m "describe the change"
git push
```

Pages redeploys automatically within a minute or so.

## Notes

- The homepage pulls its photos and the TuriTop booking widget straight from the web, so the live page looks and books exactly like the real thing.
- The booking widget uses the existing TuriTop account (`data-company="S559"`), so no booking/payment migration is involved.
- To regenerate `evaluation/index.html` after editing the Markdown: `pandoc Surf-School-Evaluation.md -s -o evaluation/index.html` (add your styling header as preferred).


================================================================
===== FILE: index.html
================================================================

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Scarborough Beach Surf School — Surf Lessons in Perth</title>
<meta name="description" content="Learn to surf at Scarborough Beach with Perth's top-rated, family-run surf school. Small groups, accredited coaches, all equipment provided. Since 1986.">
<!--
  PROOF-OF-CONCEPT facelift homepage — single file, no WordPress, no build step.
  Photos are hotlinked from the existing site CDN for demo purposes only.
  Booking uses the live TuriTop embed (company S559) — the same engine the current site uses,
  so the "Book a lesson" button opens the real booking calendar.
-->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@500;700;900&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --ink:#0c1f2c; --ink-soft:#3a4b57; --sea:#0a7ea4; --sea-deep:#075f7d;
    --sand:#f6f1e7; --sun:#ffc83d; --foam:#ffffff; --line:#e6ded0;
    --max:1180px; --r:18px;
  }
  *{box-sizing:border-box;margin:0;padding:0}
  html{scroll-behavior:smooth}
  body{font-family:Inter,system-ui,sans-serif;color:var(--ink);background:var(--foam);line-height:1.6;-webkit-font-smoothing:antialiased}
  h1,h2,h3,.display{font-family:Archivo,sans-serif;line-height:1.05;letter-spacing:-.02em}
  a{color:inherit;text-decoration:none}
  img{display:block;max-width:100%}
  .wrap{max-width:var(--max);margin:0 auto;padding:0 22px}
  .btn{display:inline-flex;align-items:center;gap:.5em;font-weight:700;font-family:Archivo;letter-spacing:.01em;
    padding:14px 26px;border-radius:999px;cursor:pointer;border:2px solid transparent;transition:.18s;font-size:1rem}
  .btn-sun{background:var(--sun);color:#1b1300}
  .btn-sun:hover{transform:translateY(-2px);box-shadow:0 10px 24px rgba(255,200,61,.4)}
  .btn-ghost{background:transparent;color:#fff;border-color:rgba(255,255,255,.55)}
  .btn-ghost:hover{background:#fff;color:var(--ink)}
  .btn-sea{background:var(--sea);color:#fff}
  .btn-sea:hover{background:var(--sea-deep)}

  /* ===== Header ===== */
  header{position:sticky;top:0;z-index:50;background:rgba(255,255,255,.92);backdrop-filter:blur(10px);border-bottom:1px solid var(--line)}
  .nav{display:flex;align-items:center;justify-content:space-between;height:70px}
  .brand{display:flex;align-items:center;gap:11px;font-family:Archivo;font-weight:900;font-size:1.05rem}
  .brand .mark{width:38px;height:38px;border-radius:10px;background:linear-gradient(135deg,var(--sea),var(--sun));display:grid;place-items:center;color:#fff;font-size:1.2rem}
  .brand small{display:block;font-family:Inter;font-weight:500;font-size:.7rem;letter-spacing:.18em;color:var(--sea);text-transform:uppercase}
  .menu{display:flex;gap:28px;font-weight:500;font-size:.95rem}
  .menu a:hover{color:var(--sea)}
  .nav .btn{padding:10px 20px;font-size:.92rem}
  .burger{display:none;font-size:1.6rem;background:none;border:0;cursor:pointer}
  @media(max-width:860px){.menu,.nav>.btn{display:none}.burger{display:block}}

  /* ===== Hero ===== */
  .hero{position:relative;min-height:88vh;display:flex;align-items:flex-end;color:#fff;overflow:hidden}
  .hero img.bg{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:-2}
  .hero::after{content:"";position:absolute;inset:0;z-index:-1;
    background:linear-gradient(180deg,rgba(8,25,38,.25) 0%,rgba(8,25,38,.15) 40%,rgba(8,25,38,.85) 100%)}
  .hero-inner{padding:60px 0 64px}
  .eyebrow{display:inline-flex;align-items:center;gap:8px;background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.3);
    padding:7px 15px;border-radius:999px;font-size:.8rem;font-weight:600;letter-spacing:.08em;text-transform:uppercase;margin-bottom:20px}
  .hero h1{font-size:clamp(2.6rem,6vw,4.6rem);font-weight:900;max-width:14ch;text-shadow:0 2px 30px rgba(0,0,0,.35)}
  .hero p.lead{font-size:clamp(1.05rem,2vw,1.3rem);max-width:46ch;margin:18px 0 28px;color:#eaf3f7}
  .hero-cta{display:flex;gap:14px;flex-wrap:wrap;align-items:center}
  .hero-meta{display:flex;gap:26px;flex-wrap:wrap;margin-top:34px;font-size:.9rem;color:#dceaf0}
  .hero-meta b{font-family:Archivo;display:block;font-size:1.5rem;color:#fff}

  /* ===== Trust strip ===== */
  .trust{background:var(--ink);color:#cfe0e8}
  .trust .wrap{display:flex;flex-wrap:wrap;gap:14px 34px;justify-content:center;padding:16px 22px;font-size:.93rem;font-weight:500}
  .trust span{display:flex;align-items:center;gap:8px}
  .trust .tick{color:var(--sun);font-weight:800}

  /* ===== Sections ===== */
  section{padding:84px 0}
  .sec-head{max-width:620px;margin-bottom:14px}
  .sec-head .kicker{color:var(--sea);font-weight:700;font-family:Archivo;letter-spacing:.12em;text-transform:uppercase;font-size:.82rem}
  .sec-head h2{font-size:clamp(2rem,4vw,2.9rem);font-weight:900;margin:10px 0 14px}
  .sec-head p{color:var(--ink-soft);font-size:1.08rem}
  .center{text-align:center;margin-inline:auto}

  /* ===== Lessons grid ===== */
  .lessons{background:var(--sand)}
  .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:24px;margin-top:42px}
  @media(max-width:900px){.grid{grid-template-columns:repeat(2,1fr)}}
  @media(max-width:600px){.grid{grid-template-columns:1fr}}
  .card{background:#fff;border-radius:var(--r);overflow:hidden;border:1px solid var(--line);
    display:flex;flex-direction:column;transition:.2s}
  .card:hover{transform:translateY(-5px);box-shadow:0 18px 40px rgba(12,31,44,.13)}
  .card .ph{position:relative;aspect-ratio:4/3;overflow:hidden}
  .card .ph img{width:100%;height:100%;object-fit:cover;transition:.4s}
  .card:hover .ph img{transform:scale(1.06)}
  .card .tag{position:absolute;top:12px;left:12px;background:var(--sun);color:#1b1300;font-family:Archivo;font-weight:700;
    font-size:.72rem;letter-spacing:.05em;text-transform:uppercase;padding:5px 11px;border-radius:999px}
  .card .body{padding:20px 20px 22px;display:flex;flex-direction:column;flex:1}
  .card h3{font-size:1.22rem;font-weight:700}
  .card .loc{color:var(--sea);font-weight:600;font-size:.82rem;letter-spacing:.06em;text-transform:uppercase;margin:4px 0 8px}
  .card p{color:var(--ink-soft);font-size:.95rem;flex:1}
  .card .foot{display:flex;align-items:center;justify-content:space-between;margin-top:16px}
  .card .price{font-family:Archivo;font-weight:900;font-size:1.25rem}
  .card .price small{font-weight:500;font-size:.72rem;color:var(--ink-soft);display:block;text-transform:uppercase;letter-spacing:.05em}
  .card .go{font-weight:700;color:var(--sea);font-size:.92rem}

  /* ===== Why / split ===== */
  .split{display:grid;grid-template-columns:1.05fr .95fr;gap:50px;align-items:center}
  @media(max-width:880px){.split{grid-template-columns:1fr;gap:30px}}
  .split img{border-radius:var(--r);width:100%;aspect-ratio:5/4;object-fit:cover;box-shadow:0 20px 50px rgba(12,31,44,.15)}
  .feat{display:grid;gap:18px;margin-top:26px}
  .feat li{list-style:none;display:flex;gap:14px;align-items:flex-start}
  .feat .ic{flex:0 0 42px;height:42px;border-radius:11px;background:#e6f4f9;color:var(--sea);display:grid;place-items:center;font-size:1.2rem}
  .feat b{font-family:Archivo}

  /* ===== Booking CTA ===== */
  .book{background:linear-gradient(135deg,var(--sea-deep),var(--sea));color:#fff;text-align:center}
  .book h2{font-size:clamp(2rem,4vw,3rem);font-weight:900;max-width:18ch;margin-inline:auto}
  .book p{max-width:48ch;margin:16px auto 30px;color:#dff0f6;font-size:1.1rem}
  .book .panel{background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.25);border-radius:var(--r);
    padding:30px;max-width:620px;margin:34px auto 0}

  /* ===== Footer ===== */
  footer{background:var(--ink);color:#aebfc9;padding:60px 0 28px;font-size:.93rem}
  .fgrid{display:grid;grid-template-columns:1.4fr 1fr 1fr;gap:36px}
  @media(max-width:760px){.fgrid{grid-template-columns:1fr;gap:26px}}
  footer h4{font-family:Archivo;color:#fff;font-size:1rem;margin-bottom:14px;letter-spacing:.04em}
  footer a:hover{color:var(--sun)}
  .fcol a{display:block;margin-bottom:8px}
  .socials{display:flex;gap:12px;margin-top:14px}
  .socials a{width:38px;height:38px;border-radius:10px;background:rgba(255,255,255,.08);display:grid;place-items:center;color:#fff;font-weight:700}
  .socials a:hover{background:var(--sea)}
  .legal{border-top:1px solid rgba(255,255,255,.12);margin-top:40px;padding-top:20px;display:flex;justify-content:space-between;flex-wrap:wrap;gap:10px;font-size:.84rem;color:#7e919c}
  .badge{display:inline-block;background:rgba(255,255,255,.08);padding:4px 12px;border-radius:999px;font-size:.78rem;margin-top:8px}
</style>
</head>
<body>

<header>
  <div class="wrap nav">
    <a class="brand" href="#top">
      <span class="mark">🌊</span>
      <span>Scarborough Beach<br><small>Surf School · Est. 1986</small></span>
    </a>
    <nav class="menu">
      <a href="#lessons">Lessons</a>
      <a href="#why">Why us</a>
      <a href="#faq">FAQ</a>
      <a href="#find">Find us</a>
    </nav>
    <a class="btn btn-sea" href="#book">Book a lesson</a>
    <button class="burger" aria-label="Menu" onclick="document.querySelector('.menu').scrollIntoView()">☰</button>
  </div>
</header>

<!-- ===== HERO ===== -->
<section class="hero" id="top">
  <img class="bg" src="https://www.surfschool.com/wp-content/uploads/2024/10/hayata-4.scarborough.jpg.webp" alt="Surfer at Scarborough Beach, Perth">
  <div class="wrap hero-inner">
    <span class="eyebrow">⭐ Perth's top-rated · family-run since 1986</span>
    <h1>Catch your first wave at Scarborough Beach</h1>
    <p class="lead">The Indian Ocean is your classroom. Fun, safe, professional surf lessons for teens and adults — complete beginners to improving surfers.</p>
    <div class="hero-cta">
      <a class="btn btn-sun" href="#book">Book online 24/7 →</a>
      <a class="btn btn-ghost" href="#lessons">See all lessons</a>
    </div>
    <div class="hero-meta">
      <div><b>4–6</b>surfers per group</div>
      <div><b>2.25 hrs</b>in the water</div>
      <div><b>All gear</b>boards + O'Neill wetsuits</div>
    </div>
  </div>
</section>

<!-- ===== TRUST ===== -->
<div class="trust">
  <div class="wrap">
    <span><span class="tick">✔</span> Accredited surf coaches</span>
    <span><span class="tick">✔</span> Small group &amp; private lessons</span>
    <span><span class="tick">✔</span> All equipment provided</span>
    <span><span class="tick">✔</span> Free easy parking</span>
    <span><span class="tick">✔</span> Perfect for tourists &amp; locals</span>
  </div>
</div>

<!-- ===== LESSONS ===== -->
<section class="lessons" id="lessons">
  <div class="wrap">
    <div class="sec-head">
      <div class="kicker">Choose your lesson</div>
      <h2>Different classes for different levels — every day</h2>
      <p>Small groups mean more waves and more one-on-one time with your instructor. Single lessons or structured multi-day courses.</p>
    </div>
    <div class="grid">

      <article class="card">
        <div class="ph"><span class="tag">Most popular</span><img src="https://www.surfschool.com/wp-content/uploads/2024/11/mylene-scarborough-2.25-hours.jpg.webp" alt="Scarborough 2.25 hour lesson"></div>
        <div class="body">
          <h3>2.25 Hour Surf Lesson</h3>
          <div class="loc">Scarborough Beach</div>
          <p>Our flagship lesson for beginners and intermediates. Early sessions for the best waves, light wind and no crowds.</p>
          <div class="foot"><div class="price">$79<small>per person</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

      <article class="card">
        <div class="ph"><span class="tag">Best value</span><img src="https://www.surfschool.com/wp-content/uploads/2024/04/scarb-2.25.jpg.webp" alt="Level 1 surf course"></div>
        <div class="body">
          <h3>Level 1 Beginner Course</h3>
          <div class="loc">Scarborough Beach</div>
          <p>2–5 lesson courses — your skills improve fast. From $59 per lesson. Up to 12 months to complete.</p>
          <div class="foot"><div class="price">$150+<small>2–5 lessons</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

      <article class="card">
        <div class="ph"><img src="https://www.surfschool.com/wp-content/uploads/2024/02/Intermediate-surfer.jpg" alt="Intermediate surfer"></div>
        <div class="body">
          <h3>Level 2 Intermediate</h3>
          <div class="loc">Scarborough Beach</div>
          <p>Small groups = more waves. Learn to read waves and surf both left and right with confidence.</p>
          <div class="foot"><div class="price">$79+<small>per person</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

      <article class="card">
        <div class="ph"><span class="tag">Winter season</span><img src="https://www.surfschool.com/wp-content/uploads/2024/10/ruby-surfing-scarboorugh-e1728542714898.jpg" alt="Leighton Beach surf lesson"></div>
        <div class="body">
          <h3>Leighton Beach Lesson</h3>
          <div class="loc">Leighton Beach</div>
          <p>2.25 hour winter lessons with a warm 4mm full-length wetsuit. Beginners and intermediates welcome.</p>
          <div class="foot"><div class="price">$79<small>per person</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

      <article class="card">
        <div class="ph"><img src="https://www.surfschool.com/wp-content/uploads/2025/10/school-holiday-classes.jpg" alt="School holiday surf lessons"></div>
        <div class="body">
          <h3>School Holiday Courses</h3>
          <div class="loc">Teens 13+</div>
          <p>Popular holiday programs for teenagers. Teaching surfing since 1986 — book online 24/7.</p>
          <div class="foot"><div class="price">From $79<small>per person</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

      <article class="card">
        <div class="ph"><span class="tag">Your own group</span><img src="https://www.surfschool.com/wp-content/uploads/2025/10/sisi-lolo-private-group.jpg.webp" alt="Private group surf lessons"></div>
        <div class="body">
          <h3>Private Group Lessons</h3>
          <div class="loc">10 years &amp; older</div>
          <p>Just your family and friends, with your own dedicated coach. Perfect for celebrations and corporate groups.</p>
          <div class="foot"><div class="price">Enquire<small>private rate</small></div><span class="go">Read more →</span></div>
        </div>
      </article>

    </div>
  </div>
</section>

<!-- ===== WHY ===== -->
<section id="why">
  <div class="wrap split">
    <div>
      <div class="sec-head">
        <div class="kicker">The iconic Scarborough surf school</div>
        <h2>Long lessons, with coaches who care</h2>
        <p>Proud to be the world's oldest surf school — a family-run business on Australia's greatest beach. The sandbanks at Scarborough make some of the best learn-to-surf conditions in the Perth metro area.</p>
      </div>
      <ul class="feat">
        <li><span class="ic">🏄</span><div><b>Small groups, more waves</b><br>Just 4–6 students per lesson — pick the best waves with real coaching time.</div></li>
        <li><span class="ic">🌅</span><div><b>Beat the crowds &amp; seabreeze</b><br>Early sessions mean clean waves, light wind, and free parking right behind our surf van.</div></li>
        <li><span class="ic">🧥</span><div><b>Top gear included</b><br>B Softboards and O'Neill wetsuits provided in every lesson.</div></li>
      </ul>
    </div>
    <img src="https://www.surfschool.com/wp-content/uploads/2024/02/teen-lessons.jpg" alt="Teenagers having fun surfing">
  </div>
</section>

<!-- ===== BOOK ===== -->
<section class="book" id="book">
  <div class="wrap">
    <h2>Ready to ride the waves?</h2>
    <p>Book your surf lesson online, any time. Lessons run daily at Scarborough or Leighton depending on conditions — we'll confirm your location by email the day before.</p>
    <a class="btn btn-sun" href="https://www.surfschool.com/book-prepaid-vouchers/" target="_blank" rel="noopener">Open the booking calendar →</a>
    <div class="panel">
      <!-- LIVE TuriTop booking widget — same engine as the current site (company S559) -->
      <div class="load-turitop" data-service="P32" data-lang="en" data-embed="box"></div>
      <p style="margin-top:14px;font-size:.85rem;color:#cfe6ef">Secure payment · gift vouchers available · 24-hour cancellation</p>
    </div>
  </div>
</section>

<!-- ===== FOOTER ===== -->
<footer id="find">
  <div class="wrap">
    <div class="fgrid">
      <div class="fcol">
        <h4>Scarborough Beach Surf School</h4>
        <p>The Esplanade, Scarborough,<br>Perth 6019, Western Australia</p>
        <p style="margin-top:10px"><a href="mailto:surf@surfschool.com">surf@surfschool.com</a><br><a href="tel:0416589141">0416 589 141</a></p>
        <span class="badge">Established 1986 · We use O'Neill wetsuits</span>
        <div class="socials">
          <a href="https://www.facebook.com/perth.surfschool/" target="_blank" rel="noopener" aria-label="Facebook">f</a>
          <a href="https://www.instagram.com/scarboroughbeachsurfschool/" target="_blank" rel="noopener" aria-label="Instagram">ig</a>
          <a href="https://www.youtube.com/channel/UCIV-VhNvyeaSX0xKNbsKCjA" target="_blank" rel="noopener" aria-label="YouTube">yt</a>
        </div>
      </div>
      <div class="fcol">
        <h4>Lessons</h4>
        <a href="#">Scarborough 2.25hr</a>
        <a href="#">Level 1 Course</a>
        <a href="#">Level 2 Course</a>
        <a href="#">Teenagers</a>
        <a href="#">School Holidays</a>
        <a href="#">Private Lessons</a>
      </div>
      <div class="fcol">
        <h4>Info</h4>
        <a href="#">FAQ</a>
        <a href="#">Surf Tips</a>
        <a href="#">Find Us</a>
        <a href="#">Contact</a>
        <a href="#">Terms &amp; Conditions</a>
        <a href="#">Privacy Policy</a>
      </div>
    </div>
    <div class="legal">
      <span>© 2026 Scarborough Beach Surf School. All rights reserved.</span>
      <span>Concept facelift — static build, no WordPress.</span>
    </div>
  </div>
</footer>

<!-- TuriTop loader (same company ID as the current live site) -->
<script src="https://app.turitop.com/js/load-turitop.min.js" data-company="S559" data-buttoncolor="green" data-ga="no"></script>
</body>
</html>


================================================================
===== FILE: Surf-School-Evaluation.md
================================================================

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


================================================================
===== FILE: REBUILD-SPEC.md
================================================================

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


================================================================
===== FILE: qwen-prompt.md
================================================================

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

