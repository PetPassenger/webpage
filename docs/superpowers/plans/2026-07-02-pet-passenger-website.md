# Pet Passenger Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 6-page static website for Pet Passenger, a local dog transportation company, using pure HTML, CSS, and vanilla JavaScript — no frameworks, no build tools.

**Architecture:** Each page is a standalone `.html` file sharing a single `style.css` stylesheet and `script.js` file. The nav and footer are hand-copied HTML snippets repeated across all pages. All interactivity (mobile nav toggle, FAQ accordion) lives in `script.js`.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, grid, `clamp()`), vanilla ES6 JavaScript, Poppins via Google Fonts CDN, Soul Gaze BV via `@font-face` local file.

## Global Constraints

- Colours: `#04042C` (navy), `#AC7D36` (gold), `#FFFFFF` (white) — no other colours
- Logo font: Soul Gaze BV — used ONLY for the "Pet Passenger" wordmark in nav and home hero, nowhere else
- All other text: Poppins — headings (700), body (400), nav/buttons (500–600)
- No external JS libraries (no jQuery, no Bootstrap, no Alpine)
- Primary CTA on every page is a phone call via `tel:` link
- Replace `000 000 0000` with the real phone number (and update the `tel:+440000000000` href to match) before launch
- Replace `hello@petpassenger.co.uk` with the real email address before launch
- Soul Gaze BV font files must be placed at `fonts/SoulGazeBV.woff2` and `fonts/SoulGazeBV.woff`
- Image filenames are listed in Task 9 Step 2 — update `src` attributes in HTML if you use different names
- Mobile-first CSS: base styles target mobile, media queries add desktop layout at `768px` and `1024px`

---

### Task 1: CSS Foundation

**Files:**
- Create: `style.css`
- Create: `fonts/` directory (place Soul Gaze BV files here)

**Interfaces:**
- Produces: CSS custom properties `--navy`, `--gold`, `--white`, `--font-main`, `--font-logo`, `--nav-height`, `--max-width`
- Produces: Utility classes `.btn`, `.btn--gold`, `.btn--outline`, `.container`, `.section`, `.section--navy`, `.section--gold`, `.section__title`, `.page-hero`, `.page-hero__bg`, `.page-hero__content`, `.card-grid`, `.card`, `.card__icon`
- Produces: Nav styles `.nav`, `.nav__inner`, `.nav__logo`, `.nav__links`, `.nav__hamburger`, `.nav__cta`
- Produces: Footer styles `.footer`, `.footer__inner`, `.footer__logo`, `.footer__slogan`, `.footer__col`, `.footer__bottom`

- [ ] **Step 1: Place Soul Gaze BV font files**

Place your Soul Gaze BV font files in:
```
fonts/SoulGazeBV.woff2
fonts/SoulGazeBV.woff
```
If you only have a `.ttf` file, use it with `format('truetype')` in the `@font-face` rule below.

- [ ] **Step 2: Create style.css**

Create `style.css` with the following complete content. Note: `@import` must appear before all other rules.

```css
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600;700&display=swap');

/* === FONTS === */
@font-face {
  font-family: 'Soul Gaze BV';
  src: url('fonts/SoulGazeBV.woff2') format('woff2'),
       url('fonts/SoulGazeBV.woff') format('woff');
  font-weight: normal;
  font-style: normal;
  font-display: swap;
}

/* === VARIABLES === */
:root {
  --navy: #04042C;
  --gold: #AC7D36;
  --white: #FFFFFF;
  --font-main: 'Poppins', sans-serif;
  --font-logo: 'Soul Gaze BV', serif;
  --max-width: 1200px;
  --nav-height: 72px;
}

/* === RESET === */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; font-size: 16px; }
body {
  font-family: var(--font-main);
  color: var(--navy);
  background: var(--white);
  padding-top: var(--nav-height);
}
img { max-width: 100%; display: block; }
a { text-decoration: none; color: inherit; }
ul { list-style: none; }

/* === TYPOGRAPHY === */
h1 { font-size: clamp(2rem, 5vw, 3.5rem); font-weight: 700; line-height: 1.15; }
h2 { font-size: clamp(1.5rem, 3vw, 2.25rem); font-weight: 700; line-height: 1.2; }
h3 { font-size: 1.2rem; font-weight: 600; }
p  { font-size: 1rem; line-height: 1.75; }

/* === BUTTONS === */
.btn {
  display: inline-block;
  padding: 0.75rem 1.75rem;
  border-radius: 4px;
  font-family: var(--font-main);
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: opacity 0.2s;
  border: none;
  line-height: 1;
}
.btn:hover { opacity: 0.85; }
.btn--gold    { background: var(--gold); color: var(--white); }
.btn--outline { background: transparent; border: 2px solid var(--gold); color: var(--gold); }

/* === LAYOUT === */
.container { max-width: var(--max-width); margin: 0 auto; padding: 0 1.5rem; }
.section { padding: 5rem 0; }
.section--navy { background: var(--navy); color: var(--white); }
.section--gold { background: var(--gold); color: var(--white); }
.section__title { text-align: center; margin-bottom: 3rem; }
.section__title h2 { margin-bottom: 0.75rem; }
.section__title p { opacity: 0.75; max-width: 600px; margin: 0 auto; }

/* === NAV === */
.nav {
  position: fixed;
  top: 0; left: 0;
  width: 100%;
  height: var(--nav-height);
  background: var(--navy);
  z-index: 1000;
  box-shadow: 0 2px 12px rgba(0,0,0,0.2);
}
.nav__inner {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 1.5rem;
  height: 100%;
  display: flex;
  align-items: center;
  gap: 1.5rem;
}
.nav__logo {
  font-family: var(--font-logo);
  color: var(--white);
  font-size: 1.75rem;
  white-space: nowrap;
  margin-right: auto;
}
.nav__links {
  display: flex;
  gap: 1.75rem;
  align-items: center;
}
.nav__links a {
  color: var(--white);
  font-size: 0.9rem;
  font-weight: 500;
  transition: color 0.2s;
}
.nav__links a:hover,
.nav__links a.active { color: var(--gold); }
.nav__cta {
  font-size: 0.85rem;
  padding: 0.55rem 1.1rem;
  white-space: nowrap;
  flex-shrink: 0;
}
.nav__hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.25rem;
  margin-left: auto;
}
.nav__hamburger span {
  display: block;
  width: 24px; height: 2px;
  background: var(--white);
  transition: transform 0.3s, opacity 0.3s;
}

/* === FOOTER === */
.footer { background: var(--navy); color: var(--white); padding-top: 4rem; }
.footer__inner {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 1.5rem 3rem;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem;
}
.footer__logo {
  font-family: var(--font-logo);
  font-size: 1.5rem;
  display: block;
  margin-bottom: 0.5rem;
}
.footer__slogan { font-size: 0.875rem; opacity: 0.7; }
.footer__col h3 {
  font-size: 0.85rem;
  font-weight: 600;
  margin-bottom: 1rem;
  color: var(--gold);
  text-transform: uppercase;
  letter-spacing: 0.06em;
}
.footer__col ul li { margin-bottom: 0.5rem; }
.footer__col a, .footer__col p { font-size: 0.875rem; opacity: 0.8; transition: opacity 0.2s; }
.footer__col a:hover { opacity: 1; }
.footer__col p { margin-bottom: 0.4rem; }
.footer__bottom {
  border-top: 1px solid rgba(255,255,255,0.1);
  text-align: center;
  padding: 1.25rem 1.5rem;
  font-size: 0.8rem;
  opacity: 0.5;
}

/* === PAGE HERO (inner pages) === */
.page-hero {
  background: var(--navy);
  color: var(--white);
  padding: 5rem 0;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.page-hero__bg {
  position: absolute;
  inset: 0;
  width: 100%; height: 100%;
  object-fit: cover;
  opacity: 0.2;
}
.page-hero__content { position: relative; z-index: 1; }
.page-hero h1 { margin-bottom: 0.75rem; }
.page-hero p { opacity: 0.75; font-size: 1.1rem; max-width: 520px; margin: 0 auto; }

/* === CARD GRID === */
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 2rem;
}
.card {
  background: var(--white);
  border-radius: 8px;
  padding: 2rem;
  box-shadow: 0 4px 20px rgba(4,4,44,0.08);
  border-top: 3px solid var(--gold);
}
.card__icon {
  width: 44px; height: 44px;
  color: var(--gold);
  margin-bottom: 1.25rem;
}
.card h3 { margin-bottom: 0.75rem; }
.card p { font-size: 0.925rem; opacity: 0.8; }

/* === CTA BANNER === */
.cta-banner {
  text-align: center;
  padding: 4rem 0;
}
.cta-banner h2 { margin-bottom: 0.75rem; }
.cta-banner p { opacity: 0.9; font-size: 1.05rem; }

/* === RESPONSIVE — NAV === */
@media (max-width: 768px) {
  .nav__hamburger { display: flex; }
  .nav__links {
    display: none;
    position: absolute;
    top: var(--nav-height);
    left: 0; width: 100%;
    flex-direction: column;
    align-items: flex-start;
    background: var(--navy);
    padding: 1rem 1.5rem 1.5rem;
    gap: 1rem;
    border-top: 1px solid rgba(255,255,255,0.1);
  }
  .nav__links.open { display: flex; }
  .nav__cta { display: none; }
}

/* === RESPONSIVE — FOOTER === */
@media (max-width: 768px) {
  .footer__inner { grid-template-columns: 1fr; gap: 2rem; }
}
```

- [ ] **Step 3: Verify file saved correctly**

Run: `wc -l style.css`
Expected: 200+ lines

---

### Task 2: Shared JavaScript

**Files:**
- Create: `script.js`

**Interfaces:**
- Consumes: `.nav__hamburger`, `.nav__links` (DOM elements present in every page's nav)
- Consumes: `.faq__item`, `.faq__question` (DOM elements present only in faq.html)
- Produces: `initNav()` — toggles class `open` on `.nav__links` and updates `aria-expanded`
- Produces: `initAccordion()` — toggles class `open` on `.faq__item`, closes all others first

- [ ] **Step 1: Create script.js**

```javascript
function initNav() {
  const hamburger = document.querySelector('.nav__hamburger');
  const links = document.querySelector('.nav__links');
  if (!hamburger || !links) return;
  hamburger.addEventListener('click', () => {
    const isOpen = links.classList.toggle('open');
    hamburger.setAttribute('aria-expanded', String(isOpen));
  });
}

function initAccordion() {
  const items = document.querySelectorAll('.faq__item');
  if (!items.length) return;
  items.forEach(item => {
    const btn = item.querySelector('.faq__question');
    btn.addEventListener('click', () => {
      const isOpen = item.classList.contains('open');
      items.forEach(i => {
        i.classList.remove('open');
        i.querySelector('.faq__question').setAttribute('aria-expanded', 'false');
      });
      if (!isOpen) {
        item.classList.add('open');
        btn.setAttribute('aria-expanded', 'true');
      }
    });
  });
}

document.addEventListener('DOMContentLoaded', () => {
  initNav();
  initAccordion();
});
```

- [ ] **Step 2: Verify file exists**

Run: `ls script.js`
Expected: `script.js`

---

### Task 3: Home Page (index.html)

**Files:**
- Modify: `index.html` (currently empty)
- Modify: `style.css` (append home-specific styles)

**Interfaces:**
- Consumes: all shared classes from `style.css` (Task 1)
- Consumes: `initNav()` from `script.js` (Task 2)

- [ ] **Step 1: Replace index.html with the home page**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pet Passenger — Safe Journeys for Your Pet</title>
  <meta name="description" content="Professional local dog transportation. Safe, insured, GPS-tracked. Call us for a quote.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html" class="active">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="pricing.html">Pricing</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li><a href="faq.html">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- HERO -->
  <section class="hero">
    <img src="images/hero.jpg" alt="Dog safely transported by Pet Passenger" class="hero__bg">
    <div class="hero__content container">
      <h1 class="hero__title">Pet Passenger</h1>
      <p class="hero__slogan">Safe Journeys for Your Pet</p>
      <a href="tel:+440000000000" class="btn btn--gold hero__cta">Call Us: 000 000 0000</a>
    </div>
  </section>

  <!-- TRUST BAR -->
  <section class="trust-bar">
    <div class="container">
      <div class="trust-bar__grid">
        <div class="trust-bar__item">
          <svg class="trust-bar__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          <span>Fully Insured</span>
        </div>
        <div class="trust-bar__item">
          <svg class="trust-bar__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="10" r="3"/><path d="M12 2a8 8 0 0 0-8 8c0 5.25 8 14 8 14s8-8.75 8-14a8 8 0 0 0-8-8z"/></svg>
          <span>GPS Tracked</span>
        </div>
        <div class="trust-bar__item">
          <svg class="trust-bar__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>
          <span>Experienced Handlers</span>
        </div>
        <div class="trust-bar__item">
          <svg class="trust-bar__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="10"/><path d="M12 8v4l3 3"/></svg>
          <span>Local &amp; Reliable</span>
        </div>
      </div>
    </div>
  </section>

  <!-- SERVICES SNAPSHOT -->
  <section class="section">
    <div class="container">
      <div class="section__title">
        <h2>What We Do</h2>
        <p>Trusted dog transportation for every journey — big or small.</p>
      </div>
      <div class="card-grid">
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
          <h3>Vet &amp; Medical Transport</h3>
          <p>Safe, stress-free rides to the vet or specialist clinic, on time, every time.</p>
        </div>
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
          <h3>Grooming &amp; Daycare</h3>
          <p>Door-to-door collection and drop-off for grooming appointments and daycare sessions.</p>
        </div>
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2"/></svg>
          <h3>Breeder &amp; Kennel Transport</h3>
          <p>Reliable, professional collection and delivery for breeders, kennels, and vet practices.</p>
        </div>
      </div>
      <div style="text-align:center; margin-top:2.5rem;">
        <a href="services.html" class="btn btn--outline">View All Services</a>
      </div>
    </div>
  </section>

  <!-- ABOUT TEASER -->
  <section class="section section--navy about-teaser">
    <div class="container about-teaser__inner">
      <div class="about-teaser__text">
        <h2>A Name You Can Trust</h2>
        <p>Pet Passenger was founded by dog lovers who understood that transporting a pet is not just a logistics problem — it's a responsibility. We treat every dog in our care as if it were our own, with calm handling, safe vehicles, and genuine compassion at every step of the journey.</p>
        <a href="about.html" class="btn btn--outline" style="margin-top:1.5rem; border-color:var(--white); color:var(--white);">Learn More About Us</a>
      </div>
      <div class="about-teaser__image">
        <img src="images/about-teaser.jpg" alt="Pet Passenger team with a dog" style="border-radius:8px; width:100%; object-fit:cover; max-height:380px;">
      </div>
    </div>
  </section>

  <!-- TESTIMONIALS -->
  <section class="section testimonials">
    <div class="container">
      <div class="section__title">
        <h2>What Our Customers Say</h2>
      </div>
      <div class="testimonials__grid">
        <blockquote class="testimonial">
          <p>"Pet Passenger took such great care of our golden retriever. He arrived calm and happy — I couldn't ask for more."</p>
          <cite>— Sarah M., dog owner</cite>
        </blockquote>
        <blockquote class="testimonial">
          <p>"We use Pet Passenger for all our kennel transfers. Punctual, professional, and the dogs always arrive stress-free."</p>
          <cite>— James L., kennels manager</cite>
        </blockquote>
        <blockquote class="testimonial">
          <p>"I was nervous about getting my rescue to the vet, but the team put both me and my dog completely at ease."</p>
          <cite>— Priya K., pet owner</cite>
        </blockquote>
      </div>
    </div>
  </section>

  <!-- CTA BANNER -->
  <section class="section--gold cta-banner">
    <div class="container">
      <h2>Ready to Book?</h2>
      <p>Get in touch today for a personal quote. We're here when you need us.</p>
      <a href="tel:+440000000000" class="btn" style="background:var(--navy);color:var(--white);margin-top:1.5rem;font-size:1.2rem;padding:1rem 2.5rem;">000 000 0000</a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append home-page styles to style.css**

```css
/* === HERO === */
.hero {
  position: relative;
  min-height: 85vh;
  display: flex;
  align-items: center;
  background-color: var(--navy);
  overflow: hidden;
}
.hero__bg {
  position: absolute;
  inset: 0;
  width: 100%; height: 100%;
  object-fit: cover;
  opacity: 0.3;
}
.hero__content {
  position: relative;
  z-index: 1;
  color: var(--white);
  padding: 5rem 1.5rem;
}
.hero__title {
  font-family: var(--font-logo);
  font-size: clamp(3.5rem, 9vw, 7rem);
  color: var(--white);
  margin-bottom: 0.75rem;
  line-height: 1;
}
.hero__slogan {
  font-family: var(--font-main);
  font-size: clamp(1.1rem, 2.5vw, 1.5rem);
  font-weight: 400;
  color: var(--gold);
  margin-bottom: 2rem;
}
.hero__cta { font-size: 1.1rem; padding: 0.9rem 2rem; }

/* === TRUST BAR === */
.trust-bar { background: var(--gold); padding: 1.75rem 0; }
.trust-bar__grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1rem;
  text-align: center;
}
.trust-bar__item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: var(--white);
  font-weight: 600;
  font-size: 0.875rem;
}
.trust-bar__icon { width: 30px; height: 30px; }

/* === ABOUT TEASER === */
.about-teaser__inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}
.about-teaser__text h2 { margin-bottom: 1.25rem; }
.about-teaser__text p { opacity: 0.85; }

/* === TESTIMONIALS === */
.testimonials__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 2rem;
}
.testimonial {
  background: var(--white);
  border-left: 4px solid var(--gold);
  padding: 1.75rem;
  border-radius: 0 8px 8px 0;
  box-shadow: 0 4px 16px rgba(4,4,44,0.07);
}
.testimonial p { font-style: italic; margin-bottom: 1rem; }
.testimonial cite { font-size: 0.875rem; color: var(--gold); font-weight: 600; font-style: normal; }

/* === RESPONSIVE — HOME === */
@media (max-width: 768px) {
  .trust-bar__grid { grid-template-columns: repeat(2, 1fr); gap: 1.25rem; }
  .about-teaser__inner { grid-template-columns: 1fr; }
  .about-teaser__image { order: -1; }
}
```

- [ ] **Step 3: Open index.html in browser and verify**

Open `index.html` (double-click or `open index.html` in Terminal). Confirm:
- "Pet Passenger" logo appears in Soul Gaze BV in the nav (a distinct decorative/script font)
- Hero shows navy background with "Pet Passenger" in Soul Gaze BV large, slogan in gold below
- Gold trust bar shows 4 items with icons
- 3 service cards with gold top border
- About teaser is 2-column on desktop
- Testimonials have gold left border
- Gold CTA banner at bottom with navy phone button
- On mobile (<768px): hamburger visible, trust bar 2-column, about teaser stacks

---

### Task 4: About Page (about.html)

**Files:**
- Create: `about.html`
- Modify: `style.css` (append about-specific styles)

**Interfaces:**
- Consumes: `.nav`, `.footer`, `.section`, `.section--navy`, `.page-hero`, `.page-hero__bg`, `.page-hero__content`, `.card-grid`, `.card`, `.card__icon`, `.container` from style.css

- [ ] **Step 1: Create about.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About Us — Pet Passenger</title>
  <meta name="description" content="Learn about Pet Passenger — who we are, our mission, and our commitment to safe dog transportation.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html" class="active">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="pricing.html">Pricing</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li><a href="faq.html">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- PAGE HERO -->
  <section class="page-hero">
    <img src="images/about-hero.jpg" alt="Pet Passenger team" class="page-hero__bg">
    <div class="page-hero__content container">
      <h1>About Us</h1>
      <p>Dog lovers who understand that every journey matters.</p>
    </div>
  </section>

  <!-- OUR STORY -->
  <section class="section">
    <div class="container story">
      <div class="story__text">
        <h2>Our Story</h2>
        <p>Pet Passenger was founded by dog owners who were frustrated by the lack of safe, reliable transport options for their pets. We knew that getting a dog to the vet, groomer, or kennel shouldn't be stressful — for the dog or the owner.</p>
        <p style="margin-top:1rem;">So we built the service we always wished existed: a calm, insured, GPS-tracked transport service staffed by people who genuinely love dogs. Today we serve individual pet owners and trade clients across the local area, one safe journey at a time.</p>
      </div>
      <div class="story__image">
        <img src="images/story.jpg" alt="Pet Passenger founder with a dog" style="border-radius:8px;width:100%;object-fit:cover;max-height:400px;">
      </div>
    </div>
  </section>

  <!-- TEAM & VEHICLES -->
  <section class="section section--navy">
    <div class="container">
      <div class="section__title">
        <h2>Our Team &amp; Vehicles</h2>
        <p>Every team member is trained in animal handling and first aid. Our vehicles are purpose-fitted with secure, ventilated crates and non-slip surfaces.</p>
      </div>
      <div class="team-grid">
        <div class="team-card">
          <img src="images/team-1.jpg" alt="Pet Passenger driver" style="width:100%;height:240px;object-fit:cover;border-radius:8px 8px 0 0;">
          <div class="team-card__body">
            <h3>Our Drivers</h3>
            <p>Experienced animal handlers who treat every dog with patience and care, no matter the journey.</p>
          </div>
        </div>
        <div class="team-card">
          <img src="images/vehicle-1.jpg" alt="Pet Passenger vehicle" style="width:100%;height:240px;object-fit:cover;border-radius:8px 8px 0 0;">
          <div class="team-card__body">
            <h3>Our Fleet</h3>
            <p>Purpose-converted vans with ventilated crates, non-slip flooring, temperature control, and GPS tracking on every journey.</p>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- VALUES -->
  <section class="section">
    <div class="container">
      <div class="section__title">
        <h2>Our Values</h2>
      </div>
      <div class="card-grid">
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>
          <h3>Safety</h3>
          <p>Every vehicle is fully insured and maintained. Every dog travels in a secure, well-ventilated crate sized for their breed.</p>
        </div>
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
          <h3>Care</h3>
          <p>We treat every dog as if it were our own — with patience, calm handling, and genuine affection at every step.</p>
        </div>
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
          <h3>Reliability</h3>
          <p>On time, every time. We know your schedule matters, and we take punctuality as seriously as you do.</p>
        </div>
        <div class="card">
          <svg class="card__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/></svg>
          <h3>Trust</h3>
          <p>Transparent pricing, honest communication, and a consistent service you can rely on again and again.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append about-page styles to style.css**

```css
/* === STORY === */
.story {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}
.story__text h2 { margin-bottom: 1.25rem; }

/* === TEAM === */
.team-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 2rem;
}
.team-card { background: rgba(255,255,255,0.07); border-radius: 8px; overflow: hidden; }
.team-card__body { padding: 1.5rem; }
.team-card__body h3 { margin-bottom: 0.5rem; color: var(--gold); }
.team-card__body p { font-size: 0.9rem; opacity: 0.85; }

/* === RESPONSIVE — ABOUT === */
@media (max-width: 768px) {
  .story { grid-template-columns: 1fr; }
  .story__image { order: -1; }
}
```

- [ ] **Step 3: Open about.html in browser and verify**

Confirm:
- "About" link is gold in the nav
- Page hero shows navy with "About Us" heading
- Story section is 2-column on desktop, single column on mobile (image above text)
- Team grid shows 2 cards on dark navy background
- 4 value cards with gold top border and gold icons
- Footer identical to home page

---

### Task 5: Services Page (services.html)

**Files:**
- Create: `services.html`
- Modify: `style.css` (append services-specific styles)

**Interfaces:**
- Consumes: `.nav`, `.footer`, `.section`, `.section--gold`, `.page-hero`, `.page-hero__bg`, `.page-hero__content`, `.container`, `.cta-banner` from style.css

- [ ] **Step 1: Create services.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Services — Pet Passenger</title>
  <meta name="description" content="Dog transportation services: vet trips, grooming, airport runs, breeder transfers, and relocation.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html" class="active">Services</a></li>
        <li><a href="pricing.html">Pricing</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li><a href="faq.html">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- PAGE HERO -->
  <section class="page-hero">
    <img src="images/services-hero.jpg" alt="Dog in Pet Passenger vehicle" class="page-hero__bg">
    <div class="page-hero__content container">
      <h1>Our Services</h1>
      <p>Safe, reliable ground transportation for dogs of all breeds and sizes.</p>
    </div>
  </section>

  <!-- INTRO + SERVICE CARDS -->
  <section class="section">
    <div class="container">
      <p class="services-intro">Whether it's a routine vet appointment or a relocation across the city, Pet Passenger provides calm, insured, GPS-tracked transport tailored to your dog's needs. We serve individual pet owners and trade clients including breeders, kennels, and veterinary practices.</p>

      <div class="services-grid">

        <div class="service-card">
          <div class="service-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M22 12h-4l-3 9L9 3l-3 9H2"/></svg>
          </div>
          <div class="service-card__body">
            <h3>Vet &amp; Medical Appointments</h3>
            <p>Safe, punctual transport to and from veterinary practices, specialist clinics, and animal hospitals. Ideal for owners who cannot drive or have anxious dogs that travel better with a calm, experienced handler.</p>
          </div>
        </div>

        <div class="service-card">
          <div class="service-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg>
          </div>
          <div class="service-card__body">
            <h3>Grooming &amp; Daycare Transport</h3>
            <p>Door-to-door collection and drop-off for grooming salons, doggy daycare, and training classes. We work around your appointment times so your dog arrives relaxed and on schedule.</p>
          </div>
        </div>

        <div class="service-card">
          <div class="service-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07A19.5 19.5 0 0 1 4.69 12a19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 3.62 1h3a2 2 0 0 1 2 1.72c.127.96.361 1.903.7 2.81a2 2 0 0 1-.45 2.11L7.91 8.6a16 16 0 0 0 6.29 6.29l.96-.96a2 2 0 0 1 2.11-.45c.907.339 1.85.573 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
          </div>
          <div class="service-card__body">
            <h3>Airport &amp; Travel Runs</h3>
            <p>Timely, stress-free transport to airports, train stations, and travel hubs when your itinerary requires your dog to be somewhere specific at a specific time.</p>
          </div>
        </div>

        <div class="service-card">
          <div class="service-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2"/></svg>
          </div>
          <div class="service-card__body">
            <h3>Breeder &amp; Kennel Transport</h3>
            <p>Reliable, professional collection and delivery for breeders, boarding kennels, and vet practices. We handle multiple dogs on scheduled routes — contact us to discuss regular trade bookings and rates.</p>
          </div>
        </div>

        <div class="service-card">
          <div class="service-card__icon">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>
          </div>
          <div class="service-card__body">
            <h3>Dog Relocation</h3>
            <p>Moving home? We'll transport your dog safely while you manage the move. Perfect for longer local journeys where a calm, focused ride matters most.</p>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- CTA -->
  <section class="section--gold cta-banner">
    <div class="container">
      <h2>Need Something Different?</h2>
      <p>Call us — we're happy to discuss bespoke requirements.</p>
      <a href="tel:+440000000000" class="btn" style="background:var(--navy);color:var(--white);margin-top:1.5rem;font-size:1.1rem;padding:0.9rem 2rem;">000 000 0000</a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append services styles to style.css**

```css
/* === SERVICES === */
.services-intro {
  max-width: 720px;
  font-size: 1.05rem;
  line-height: 1.8;
  text-align: center;
  margin: 0 auto 3rem;
}
.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.75rem;
}
.service-card {
  display: flex;
  gap: 1.25rem;
  padding: 1.75rem;
  border-radius: 8px;
  box-shadow: 0 4px 20px rgba(4,4,44,0.08);
  border-left: 4px solid var(--gold);
}
.service-card__icon {
  flex-shrink: 0;
  width: 40px; height: 40px;
  color: var(--gold);
}
.service-card__icon svg { width: 100%; height: 100%; }
.service-card__body h3 { margin-bottom: 0.6rem; }
.service-card__body p { font-size: 0.9rem; opacity: 0.8; }

@media (max-width: 600px) {
  .service-card { flex-direction: column; }
}
```

- [ ] **Step 3: Open services.html in browser and verify**

Confirm:
- "Services" is gold in the nav
- Intro paragraph is centred with wider max-width
- 5 service cards with gold left border, icon left / text right on desktop
- Cards stack (icon above text) on mobile
- Gold CTA banner at bottom

---

### Task 6: Pricing Page (pricing.html)

**Files:**
- Create: `pricing.html`
- Modify: `style.css` (append pricing-specific styles)

**Interfaces:**
- Consumes: `.nav`, `.footer`, `.section`, `.page-hero`, `.page-hero__content`, `.container`, `.btn--gold` from style.css

- [ ] **Step 1: Create pricing.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Pricing — Pet Passenger</title>
  <meta name="description" content="Get a quote for dog transportation. Call us for fast, bespoke pricing based on your journey.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="pricing.html" class="active">Pricing</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li><a href="faq.html">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- PAGE HERO -->
  <section class="page-hero">
    <div class="page-hero__content container">
      <h1>Pricing &amp; Get a Quote</h1>
      <p>All pricing is tailored to your journey. Call us for a fast, no-obligation quote.</p>
    </div>
  </section>

  <!-- PRICING CONTENT -->
  <section class="section">
    <div class="container pricing-content">

      <div class="pricing-statement">
        <h2>Bespoke Pricing for Every Journey</h2>
        <p>We don't believe in one-size-fits-all pricing. Every dog, every route, and every journey is different — so our quotes reflect exactly what your trip requires. Pricing is based on:</p>
        <ul class="pricing-factors">
          <li>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="10" r="3"/><path d="M12 2a8 8 0 0 0-8 8c0 5.25 8 14 8 14s8-8.75 8-14a8 8 0 0 0-8-8z"/></svg>
            <span><strong>Distance</strong> — from collection point to destination</span>
          </li>
          <li>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M20.84 4.61a5.5 5.5 0 0 0-7.78 0L12 5.67l-1.06-1.06a5.5 5.5 0 0 0-7.78 7.78l1.06 1.06L12 21.23l7.78-7.78 1.06-1.06a5.5 5.5 0 0 0 0-7.78z"/></svg>
            <span><strong>Dog size &amp; number</strong> — breed, weight, and number of dogs travelling</span>
          </li>
          <li>
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
            <span><strong>Journey type</strong> — single trip, return, or regular standing booking</span>
          </li>
        </ul>
      </div>

      <div class="pricing-cta-box">
        <h2>Get Your Quote</h2>
        <p>The fastest way to get a price is to give us a call. We'll ask a few quick questions and give you a clear, no-obligation quote on the spot.</p>
        <a href="tel:+440000000000" class="btn btn--gold pricing-phone">000 000 0000</a>
        <p class="pricing-email-note">Prefer email? We'll get back to you within a few hours.</p>
        <a href="mailto:hello@petpassenger.co.uk" class="pricing-email-link">hello@petpassenger.co.uk</a>
      </div>

    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append pricing styles to style.css**

```css
/* === PRICING === */
.pricing-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}
.pricing-statement h2 { margin-bottom: 1.25rem; }
.pricing-statement > p { margin-bottom: 1.5rem; }
.pricing-factors { display: flex; flex-direction: column; gap: 1rem; }
.pricing-factors li {
  display: flex;
  align-items: flex-start;
  gap: 0.75rem;
  font-size: 0.95rem;
  line-height: 1.5;
}
.pricing-factors li svg { width: 20px; height: 20px; color: var(--gold); flex-shrink: 0; margin-top: 2px; }

.pricing-cta-box {
  background: var(--navy);
  color: var(--white);
  padding: 2.5rem;
  border-radius: 8px;
  text-align: center;
}
.pricing-cta-box h2 { margin-bottom: 1rem; }
.pricing-cta-box > p { opacity: 0.85; margin-bottom: 2rem; font-size: 0.95rem; }
.pricing-phone {
  font-size: 1.4rem;
  padding: 1rem 2.5rem;
  display: block;
  width: 100%;
  text-align: center;
}
.pricing-email-note { margin-top: 1.5rem; margin-bottom: 0.5rem; font-size: 0.875rem; opacity: 0.7; }
.pricing-email-link { color: var(--gold); font-size: 0.95rem; font-weight: 500; }
.pricing-email-link:hover { text-decoration: underline; }

@media (max-width: 768px) {
  .pricing-content { grid-template-columns: 1fr; gap: 2.5rem; }
}
```

- [ ] **Step 3: Open pricing.html in browser and verify**

Confirm:
- "Pricing" is gold in the nav
- Two-column layout: pricing factors left, navy quote box right
- Gold phone button is full-width inside the navy box
- Email link appears in gold below
- Single column on mobile

---

### Task 7: Contact Page (contact.html)

**Files:**
- Create: `contact.html`
- Modify: `style.css` (append contact-specific styles)

**Interfaces:**
- Consumes: `.nav`, `.footer`, `.section`, `.page-hero`, `.page-hero__content`, `.container` from style.css

- [ ] **Step 1: Create contact.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact — Pet Passenger</title>
  <meta name="description" content="Contact Pet Passenger. Call 000 000 0000 or email hello@petpassenger.co.uk for dog transportation.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="pricing.html">Pricing</a></li>
        <li><a href="contact.html" class="active">Contact</a></li>
        <li><a href="faq.html">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- PAGE HERO -->
  <section class="page-hero">
    <div class="page-hero__content container">
      <h1>Contact Us</h1>
      <p>We're here to help. The quickest way to reach us is by phone.</p>
    </div>
  </section>

  <!-- CONTACT INFO -->
  <section class="section">
    <div class="container contact-layout">

      <div class="contact-primary">
        <h2>Get in Touch</h2>
        <p>For bookings, quotes, or any questions, call us directly. We aim to answer every call during business hours.</p>
        <a href="tel:+440000000000" class="contact-phone">000 000 0000</a>
        <div class="contact-details">
          <div class="contact-detail">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
            <div>
              <strong>Email</strong>
              <a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a>
            </div>
          </div>
          <div class="contact-detail">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>
            <div>
              <strong>Hours</strong>
              <span>Monday – Saturday: 7am – 7pm</span>
              <span>Sunday: 9am – 5pm</span>
            </div>
          </div>
          <div class="contact-detail">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="10" r="3"/><path d="M12 2a8 8 0 0 0-8 8c0 5.25 8 14 8 14s8-8.75 8-14a8 8 0 0 0-8-8z"/></svg>
            <div>
              <strong>Service Area</strong>
              <span>Serving [Your City] and surrounding areas</span>
            </div>
          </div>
        </div>
      </div>

      <div class="contact-map">
        <!--
          To embed Google Maps:
          1. Go to maps.google.com → search your location → Share → Embed a map
          2. Copy the <iframe> code and replace this comment with it
        -->
        <div class="map-placeholder">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" style="width:48px;height:48px;opacity:0.4;margin-bottom:1rem;"><circle cx="12" cy="10" r="3"/><path d="M12 2a8 8 0 0 0-8 8c0 5.25 8 14 8 14s8-8.75 8-14a8 8 0 0 0-8-8z"/></svg>
          <p>Map coming soon</p>
          <p style="font-size:0.875rem;margin-top:0.5rem;">Serving [Your City] and surrounding areas</p>
        </div>
      </div>

    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append contact styles to style.css**

```css
/* === CONTACT === */
.contact-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: start;
}
.contact-primary h2 { margin-bottom: 1rem; }
.contact-primary > p { margin-bottom: 2rem; }
.contact-phone {
  display: block;
  font-size: clamp(2rem, 5vw, 3rem);
  font-weight: 700;
  color: var(--gold);
  margin-bottom: 2.5rem;
  line-height: 1;
}
.contact-phone:hover { text-decoration: underline; }
.contact-details { display: flex; flex-direction: column; gap: 1.5rem; }
.contact-detail { display: flex; gap: 1rem; align-items: flex-start; }
.contact-detail svg { width: 22px; height: 22px; color: var(--gold); flex-shrink: 0; margin-top: 3px; }
.contact-detail div { display: flex; flex-direction: column; gap: 0.2rem; }
.contact-detail strong { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.06em; color: var(--navy); }
.contact-detail a, .contact-detail span { font-size: 0.95rem; color: var(--navy); }
.contact-detail a:hover { color: var(--gold); }

.contact-map { border-radius: 8px; overflow: hidden; min-height: 380px; }
.contact-map iframe { width: 100%; min-height: 380px; border: 0; display: block; border-radius: 8px; }
.map-placeholder {
  background: #f4f4f4;
  min-height: 380px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  color: #888;
  text-align: center;
  padding: 2rem;
}

@media (max-width: 768px) {
  .contact-layout { grid-template-columns: 1fr; }
  .contact-phone { font-size: 2.25rem; }
}
```

- [ ] **Step 3: Open contact.html in browser and verify**

Confirm:
- "Contact" is gold in the nav
- Phone number is large in gold, clickable (`tel:` link)
- Three contact detail rows (email, hours, service area) with gold icons
- Map placeholder is visible (right column on desktop, below on mobile)

---

### Task 8: FAQ Page (faq.html)

**Files:**
- Create: `faq.html`
- Modify: `style.css` (append FAQ-specific styles)

**Interfaces:**
- Consumes: `.nav`, `.footer`, `.section`, `.section--gold`, `.page-hero`, `.page-hero__content`, `.container`, `.cta-banner` from style.css
- Consumes: `initAccordion()` from `script.js` — targets `.faq__item` and `.faq__question`
- Class `.faq__item.open` is toggled by JS; CSS uses it to expand `.faq__answer` via `max-height`

- [ ] **Step 1: Create faq.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>FAQ — Pet Passenger</title>
  <meta name="description" content="Frequently asked questions about Pet Passenger dog transportation.">
  <link rel="stylesheet" href="style.css">
</head>
<body>

  <!-- NAV -->
  <nav class="nav">
    <div class="nav__inner">
      <a href="index.html" class="nav__logo">Pet Passenger</a>
      <button class="nav__hamburger" aria-label="Toggle menu" aria-expanded="false">
        <span></span><span></span><span></span>
      </button>
      <ul class="nav__links">
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="pricing.html">Pricing</a></li>
        <li><a href="contact.html">Contact</a></li>
        <li><a href="faq.html" class="active">FAQ</a></li>
      </ul>
      <a href="tel:+440000000000" class="btn btn--gold nav__cta">Call Us: 000 000 0000</a>
    </div>
  </nav>

  <!-- PAGE HERO -->
  <section class="page-hero">
    <div class="page-hero__content container">
      <h1>Frequently Asked Questions</h1>
      <p>Everything you need to know before booking with Pet Passenger.</p>
    </div>
  </section>

  <!-- FAQ ACCORDION -->
  <section class="section">
    <div class="container faq-container">

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          What breeds and sizes do you transport?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>We transport dogs of all breeds and sizes, from small toy breeds to large dogs like Great Danes and Newfoundlands. We match the right crate size to your dog to ensure a safe, comfortable journey. If you have a particularly large or unusual breed, let us know when you call.</p>
        </div>
      </div>

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          Are you insured?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>Yes. Pet Passenger holds full public liability insurance and specialist animal-in-transit insurance. All our vehicles and drivers are covered for the transportation of animals. We're happy to provide documentation on request.</p>
        </div>
      </div>

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          How far in advance should I book?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>We recommend booking at least 48 hours in advance to guarantee your preferred time slot. For regular bookings — weekly vet trips, recurring grooming runs — we can set up a standing schedule. We do occasionally have same-day availability, so call us to check.</p>
        </div>
      </div>

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          What happens if my dog gets anxious during travel?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>All our drivers are trained in calm animal handling. We use covered, ventilated crates which many anxious dogs find reassuring. For dogs with known travel anxiety, we recommend bringing a familiar blanket or toy. If you're concerned, let us know when booking and we'll take extra care. We do not administer sedatives — if your vet recommends this, please advise us in advance.</p>
        </div>
      </div>

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          Do you transport multiple dogs at once?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>Yes — we can transport multiple dogs in the same booking, whether from the same household or for trade clients such as breeders and kennels. Each dog travels in their own secure crate. Contact us to discuss multi-dog bookings and trade rates.</p>
        </div>
      </div>

      <div class="faq__item">
        <button class="faq__question" aria-expanded="false">
          How is pricing calculated?
          <svg class="faq__chevron" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><polyline points="6 9 12 15 18 9"/></svg>
        </button>
        <div class="faq__answer">
          <p>Pricing is bespoke and based on distance, the number and size of dogs, and the type of journey (single, return, or regular booking). We don't publish fixed tariffs because every journey is different. Call us and we'll give you a clear, no-obligation quote in minutes.</p>
        </div>
      </div>

    </div>
  </section>

  <!-- CTA -->
  <section class="section--gold cta-banner">
    <div class="container">
      <h2>Still Have Questions?</h2>
      <p>We're happy to chat through your requirements — no obligation.</p>
      <a href="tel:+440000000000" class="btn" style="background:var(--navy);color:var(--white);margin-top:1.5rem;font-size:1.1rem;padding:0.9rem 2rem;">000 000 0000</a>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer">
    <div class="footer__inner">
      <div class="footer__col">
        <span class="footer__logo">Pet Passenger</span>
        <p class="footer__slogan">Safe Journeys for Your Pet</p>
      </div>
      <div class="footer__col">
        <h3>Quick Links</h3>
        <ul>
          <li><a href="index.html">Home</a></li>
          <li><a href="about.html">About</a></li>
          <li><a href="services.html">Services</a></li>
          <li><a href="pricing.html">Pricing</a></li>
          <li><a href="contact.html">Contact</a></li>
          <li><a href="faq.html">FAQ</a></li>
        </ul>
      </div>
      <div class="footer__col">
        <h3>Contact</h3>
        <p><a href="tel:+440000000000">000 000 0000</a></p>
        <p><a href="mailto:hello@petpassenger.co.uk">hello@petpassenger.co.uk</a></p>
      </div>
    </div>
    <div class="footer__bottom">
      <p>&copy; 2026 Pet Passenger. All rights reserved.</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Append FAQ styles to style.css**

```css
/* === FAQ === */
.faq-container { max-width: 780px; margin: 0 auto; }
.faq__item { border-bottom: 1px solid rgba(4,4,44,0.12); }
.faq__item:first-child { border-top: 1px solid rgba(4,4,44,0.12); }
.faq__question {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 0;
  background: none;
  border: none;
  cursor: pointer;
  font-family: var(--font-main);
  font-size: 1rem;
  font-weight: 600;
  color: var(--navy);
  text-align: left;
  gap: 1rem;
}
.faq__question:hover { color: var(--gold); }
.faq__chevron {
  width: 20px; height: 20px;
  flex-shrink: 0;
  transition: transform 0.3s;
  color: var(--gold);
}
.faq__item.open .faq__chevron { transform: rotate(180deg); }
.faq__answer {
  max-height: 0;
  overflow: hidden;
  transition: max-height 0.35s ease;
}
.faq__item.open .faq__answer { max-height: 400px; }
.faq__answer p {
  padding-bottom: 1.5rem;
  font-size: 0.95rem;
  opacity: 0.8;
  line-height: 1.75;
}
```

- [ ] **Step 3: Open faq.html in browser and verify accordion**

Confirm:
- "FAQ" is gold in the nav
- All 6 items show their questions, collapsed by default
- Clicking a question smoothly expands its answer
- Clicking a second question collapses the first and opens the second
- Chevron rotates 180° on open items
- Gold CTA banner at bottom

---

### Task 9: Final Review &amp; Launch Checklist

**Files:**
- Modify: all 6 HTML files (real content), `images/` directory (real photos)

**Interfaces:**
- Consumes: all pages created in Tasks 3–8

- [ ] **Step 1: Replace all placeholder content**

Search every HTML file for these strings and replace:

| Find | Replace with |
|------|-------------|
| `000 000 0000` | real phone number |
| `tel:+440000000000` | `tel:+44XXXXXXXXXX` (E.164 format, no spaces) |
| `hello@petpassenger.co.uk` | real email address |
| `[Your City]` | real city/area name |
| `[X] miles` | real coverage radius |
| `2026` (copyright) | current year if different |

- [ ] **Step 2: Add real images to images/ directory**

Place images with these exact filenames (or update `src` attributes in the HTML if you use different names):

| File | Used on |
|------|---------|
| `images/hero.jpg` | index.html hero section |
| `images/about-teaser.jpg` | index.html about teaser |
| `images/about-hero.jpg` | about.html page hero |
| `images/story.jpg` | about.html our story section |
| `images/team-1.jpg` | about.html team &amp; vehicles |
| `images/vehicle-1.jpg` | about.html team &amp; vehicles |
| `images/services-hero.jpg` | services.html page hero |

All images should be web-optimised (JPEG, max 200KB each). Recommended tool: squoosh.app

- [ ] **Step 3: Verify Soul Gaze BV font loads**

Open any page in Chrome → DevTools (F12) → Network tab → reload → filter by "Font". Confirm `SoulGazeBV.woff2` appears with status 200. If it shows 404, check that the file is at `fonts/SoulGazeBV.woff2` relative to the HTML files.

- [ ] **Step 4: Cross-page navigation check**

Open `index.html` and click every nav link in order. On each page confirm:
- The correct nav link is gold (`.active` class)
- The "Call Us" button in the nav is visible on desktop
- The footer phone and email links are correct

- [ ] **Step 5: Mobile check**

Open Chrome DevTools → toggle device toolbar (Cmd+Shift+M) → set width to 375px. On each page confirm:
- Hamburger icon is visible, nav links are hidden
- Tapping hamburger opens a vertical dropdown
- Hero text and CTA are readable, nothing overflows
- Service/value/testimonial cards stack vertically
- Footer stacks to a single column

- [ ] **Step 6: Accessibility spot-check**

- All content `<img>` tags have descriptive `alt` text (not empty)
- Tab through each page: all links and buttons are keyboard-focusable
- FAQ: `aria-expanded` attribute updates correctly when items open/close (check in DevTools → Elements)

- [ ] **Step 7: Deploy**

Choose one of:
- **Netlify (easiest):** Drag the project folder to app.netlify.com drop zone
- **GitHub Pages:** Push to GitHub repo → Settings → Pages → Branch: main / root
- **Vercel:** `npx vercel` in project folder (requires Node.js installed)
- **Traditional hosting:** Upload all files via FTP/SFTP to the web root

---

## Spec Coverage

| Spec requirement | Covered |
|---|---|
| Home: hero, trust bar, services snapshot, about teaser, testimonials, CTA banner | Task 3 |
| About: page hero, story, team/vehicles, 4 values | Task 4 |
| Services: intro, 5 service cards | Task 5 |
| Pricing: bespoke statement, phone CTA, email CTA | Task 6 |
| Contact: phone large, email, hours, service area, map slot | Task 7 |
| FAQ: 6-item accordion | Task 8 |
| Shared nav: Soul Gaze BV logo, links, Call Us button, hamburger | Tasks 1–3 |
| Shared footer: 3 columns, copyright | Tasks 1–3 |
| Colours `#04042C`, `#AC7D36`, `#FFFFFF` only | Task 1 (CSS variables, no other colours) |
| Soul Gaze BV logo only, Poppins everywhere else | Task 1 |
| Mobile-first responsive at 768px | Tasks 1–8 (every task includes media queries) |
| No frameworks, no build tools | All tasks — plain HTML/CSS/JS |
| Primary CTA is a phone call on every page | Tasks 3–8 |
| Smooth scroll | Task 1 (`scroll-behavior: smooth` on `html`) |
| Nav toggle JS | Task 2 |
| FAQ accordion JS (one open at a time) | Task 2 + Task 8 |
