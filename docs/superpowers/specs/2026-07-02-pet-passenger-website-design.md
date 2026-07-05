# Pet Passenger — Static Website Design Spec

**Date:** 2026-07-02
**Project:** Pet Passenger static website
**Approach:** Pure HTML/CSS/JS, 6-page site, no build tools or frameworks

---

## 1. Business Context

Pet Passenger is a local dog transportation company offering ground-only, same-day transport within a city/local area. It serves a mixed audience of individual pet owners (families, people moving or travelling) and professional B2B clients (breeders, kennels, veterinary clinics).

The primary conversion action is a phone call. Pricing is bespoke and communicated by phone or email — there is no online booking or price calculator.

---

## 2. Brand Identity

### Slogan
> Safe Journeys for Your Pet

### Colours
| Role | Hex | Usage |
|------|-----|-------|
| Deep Navy | `#04042C` | Header, footer, section backgrounds, headings |
| Warm Gold | `#AC7D36` | Buttons, hover states, accents, dividers |
| White | `#FFFFFF` | Body backgrounds, body text on dark sections |

### Typography
| Use | Font | Weight |
|-----|------|--------|
| Logo wordmark ("Pet Passenger") | Soul Gaze BV | Regular |
| Slogan, headings, body, nav, buttons | Poppins | Bold (headings), Regular (body) |

Soul Gaze BV is used exclusively for the logo wordmark. Poppins handles all other text across the site.

### Visual Tone
Trustworthy, warm, professional. Navy signals reliability; gold signals care and premium quality. Avoids playful pastels — positions Pet Passenger as a serious, dependable service suitable for both individual owners and trade clients.

---

## 3. File Structure

```
/
├── index.html          Home
├── about.html          About Us
├── services.html       Services
├── pricing.html        Pricing / Get a Quote
├── contact.html        Contact
├── faq.html            FAQ
├── style.css           Shared stylesheet
├── script.js           Shared JS (nav toggle, FAQ accordion)
└── images/             All photos (real photography provided)
```

---

## 4. Shared Components

### Navigation (fixed top bar)
- Background: `#04042C`
- Left: "Pet Passenger" wordmark in Soul Gaze BV, white
- Right: nav links in Poppins — Home, About, Services, Pricing, Contact, FAQ
- Far right: gold "Call Us" button with phone number — always visible on desktop
- Mobile: hamburger icon collapses nav links into a vertical dropdown

### Footer
- Background: `#04042C`
- Three columns: Logo + slogan | Quick links | Contact details (phone, email)
- Bottom bar: copyright line in small Poppins text

---

## 5. Page Designs

### Home (`index.html`)
1. **Hero** — Full-width real photo, navy overlay, "Pet Passenger" wordmark large in Soul Gaze BV, slogan in Poppins beneath, gold "Call Us" CTA button
2. **Trust bar** — 4 icon+text pillars: "Fully Insured", "GPS Tracked", "Experienced Handlers", "Local & Reliable"
3. **Services snapshot** — 3 cards (icon, title, one-line description), linking to services.html
4. **About teaser** — Short paragraph + photo, "Learn More" link to about.html
5. **Testimonials** — 2–3 customer quotes, navy background
6. **CTA banner** — Gold background, "Ready to book?" + large phone number

### About (`about.html`)
1. **Page hero** — Title + background photo
2. **Our story** — Who Pet Passenger is, mission statement, operating history
3. **Team & vehicles** — Photos of team or van with short descriptions
4. **Values** — 4 pillars with icons: Safety, Care, Reliability, Trust

### Services (`services.html`)
1. **Intro paragraph** — Overview of what Pet Passenger offers
2. **Service cards** (icon, title, short description, gold accent):
   - Vet & medical appointment transport
   - Grooming & daycare transport
   - Airport & travel runs
   - Breeder & kennel transport (B2B)
   - Dog relocation (moving home)

### Pricing / Get a Quote (`pricing.html`)
1. **Bespoke pricing statement** — Clear explanation that pricing depends on distance, dog size, and journey type
2. **Example price ranges** (optional) — 2–3 ranges to set expectations and build trust
3. **Primary CTA** — "Call us for a quote" with phone number large and prominent
4. **Secondary CTA** — Email address for non-urgent enquiries

### Contact (`contact.html`)
1. **Phone number** — Large, prominent, above the fold
2. **Email address**
3. **Operating hours**
4. **Service area** — Text description (e.g. "Serving Greater London") and/or embedded Google Map

### FAQ (`faq.html`)
1. **Accordion-style Q&A** (JS toggle, one item open at a time):
   - What breeds and sizes do you transport?
   - Are you insured?
   - How far in advance should I book?
   - What happens if my dog gets anxious during travel?
   - Do you transport multiple dogs at once?
   - How is pricing calculated?

---

## 6. Interactions & JS

- **Nav toggle:** Hamburger button shows/hides nav links on mobile
- **FAQ accordion:** Click to expand/collapse individual answers; only one open at a time
- **Smooth scroll:** Anchor links scroll smoothly (CSS `scroll-behavior: smooth` sufficient)
- No third-party JS libraries required

---

## 7. Responsiveness

- Mobile-first CSS
- Breakpoints: mobile (<768px), tablet (768px–1024px), desktop (>1024px)
- Nav collapses to hamburger on mobile
- Service/value cards stack vertically on mobile
- Hero text and CTA scale down on smaller screens

---

## 8. Assets

- **Photography:** Real photos provided by client (vehicles, team, dogs in transport)
- **Icons:** Simple SVG icons for trust bar, service cards, value pillars (can use free icon set e.g. Heroicons or hand-coded SVGs)
- **Fonts:** Soul Gaze BV loaded via `@font-face` (local file); Poppins via Google Fonts CDN

---

## 9. Hosting

Static files — compatible with any host: GitHub Pages, Netlify, Vercel, or traditional shared hosting. No server-side logic required.
