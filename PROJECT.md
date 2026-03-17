# Body Mind Healing — Project Documentation

## About
Website for **Tamara Hofland-Doloechanova**, holistic therapist based in Almere, The Netherlands. Bilingual (Polish/English) static site.

**Live site:** https://tamarahealing.pl

---

## Architecture

### Hosting
- **GitHub Pages** — static site served from `main` branch
- **Repository:** github.com/SysFormer/tamarahealing-webpage
- **CI/CD:** Push to `main` = automatic deploy
- **SSL:** Let's Encrypt (auto-provisioned by GitHub Pages)
- **Domain:** tamarahealing.pl (registered via VDX, mijn.vdx.nl)

### Stack
- Pure HTML/CSS/JavaScript (no build tools, no frameworks)
- Google Fonts (Cormorant Garamond + Nunito Sans)
- Web3Forms for contact form
- hCaptcha for spam protection

---

## Pages

| File | Description |
|---|---|
| `index.html` | Landing page — hero, about Tamara, 4 services (expandable), 28 testimonials carousel, contact form |
| `reconnection.html` | Reconnection & Reconnective Healing by Eric Pearl — detailed service page with pricing, "Why 333?", YouTube videos |
| `gdv-camera.html` | GDV Camera / Kirlian Effect diagnostics — Prof. Korotkov method, images from original doc, YouTube video |
| `vedapulse.html` | VedaPulse pulse diagnostics — Oleg Sorokin, what it measures, YouTube video |
| `gallery.html` | Photo gallery with lightbox — 12+ photos of Tamara with mentors and at conferences |
| `cv.html` | Full curriculum vitae — education, experience, all certifications |
| `privacy-policy.html` | GDPR-compliant privacy policy (Dutch law) |
| `terms.html` | Terms of use — informational purpose, no medical advice disclaimer |

---

## Directory Structure

```
tamara/
├── index.html              # Main landing page
├── reconnection.html       # Reconnection service page
├── gdv-camera.html         # GDV Camera service page
├── vedapulse.html          # VedaPulse service page
├── gallery.html            # Photo gallery
├── cv.html                 # Curriculum Vitae
├── privacy-policy.html     # Privacy policy
├── terms.html              # Terms of use
├── CNAME                   # Custom domain (tamarahealing.pl)
├── .gitignore              # Excludes designs/, docs/, mockups/
├── PROJECT.md              # This file
├── assets/                 # Design assets (deployed)
│   ├── logo.png
│   ├── hero-bg.png
│   ├── about-bg.png
│   ├── texture.png
│   ├── testimonial-bg.png
│   └── services-icon.png
├── photos/                 # All photos (deployed)
│   ├── viber_image_2026-03-16_16-52-28-568.jpg  # Tamara main photo
│   ├── indepenttrader-trader21-cezary-gluch-690x434.webp  # Featured testimonial
│   ├── gdv-kirlian-couple.jpg    # Extracted from GDV doc
│   ├── gdv-finger-glow.jpg      # Extracted from GDV doc
│   ├── gdv-pre-post-aura.jpg    # Extracted from GDV doc
│   ├── Eric Pearl.jpg
│   ├── Reconnection.JPG
│   ├── Prof. K. Korotkov.JPG
│   ├── K.Korotkov.jpg
│   ├── Frank Kinslow.JPG
│   ├── Mantak Chia.JPG
│   ├── O. Sorokin.jpg
│   └── ... (more gallery photos)
├── designs/                # Ideogram-generated assets (GITIGNORED)
├── docs/                   # Original .doc files from Tamara (GITIGNORED)
├── mockups/                # Design variants A, B, C (GITIGNORED)
└── ideogram-prompts.md     # Prompts used to generate design assets
```

---

## Design System

### Visual Identity: "Pełne Zanurzenie" (Full Immersion)
Dark, cinematic, immersive. Plum backgrounds with gold accents and cream text.

### Colors
| Role | Hex |
|---|---|
| Primary Gold | `#C8963E` |
| Secondary Amber | `#D4A855` |
| Accent Violet | `#7B6D8E` |
| Deep Plum | `#4A3B5C` |
| Background Cream | `#FFF8EE` |
| Background Off-white | `#FFFDF9` |
| Text Primary | `#3A2E2A` |
| Text Secondary | `#6B5D56` |

### Typography
- **Headings:** Cormorant Garamond (Medium/SemiBold)
- **Body:** Nunito Sans (Regular 400, SemiBold 600)

---

## Internationalization (i18n)

All pages support Polish (default) and English via a language toggle in the nav.

**Implementation:**
- HTML elements have `data-i18n="key"` attributes
- JavaScript `T` object contains `pl` and `en` translation maps
- `setLang(lang)` function loops through elements and sets `innerHTML`
- Testimonials stored in JS array with `pl` and `en` properties

---

## Contact Form

### Provider: Web3Forms
- **Access key:** `a59136a1-0369-424f-aba8-8d747b1bed0d`
- **Recipient:** tamara@bodymindhealing.nl
- **Dashboard:** https://app.web3forms.com/
- **Free tier:** 250 submissions/month

### How it works
1. User fills form + completes hCaptcha
2. JS builds a temporary `<form>` element with hidden fields
3. Native POST to `https://api.web3forms.com/submit`
4. Web3Forms sends email to Tamara
5. Redirects back to site with `?sent=1#kontakt`
6. JS detects `?sent=1` and shows success message

### Spam protection
- hCaptcha widget (loaded via `web3forms.com/client/script.js`)
- GDPR consent checkbox (required)

---

## DNS Configuration

**Registrar:** VDX (mijn.vdx.nl)

| Name | Type | Value |
|---|---|---|
| @ | A | 185.199.108.153 |
| @ | A | 185.199.109.153 |
| @ | A | 185.199.110.153 |
| @ | A | 185.199.111.153 |
| @ | AAAA | 2606:50c0:8000::153 |
| @ | AAAA | 2606:50c0:8001::153 |
| @ | AAAA | 2606:50c0:8002::153 |
| @ | AAAA | 2606:50c0:8003::153 |
| www | CNAME | sysflow-it.github.io |
| mail | A | 91.142.254.97 |
| @ | MX (10) | mail.tamarahealing.pl |
| @ | TXT | SPF record |
| _dmarc | TXT | DMARC record |
| _github-pages-challenge-sysflow-it | TXT | GitHub verification |

**Known issues resolved:**
- VDX auto-injected a hidden AAAA record → had to ask support to remove
- DNSSEC was in error state → asked VDX to fix
- Wildcard `*` A record was interfering → deleted

---

## Tamara's Services (on site)

1. **Psychoterapia Integracyjna** — Personality disorders, depression, anxiety, trauma, PTSD, grief, relationship issues. Methods: EMDR, EFT, TAT, TFT, WHEE, Rebirthing, Mindfulness.

2. **Dolegliwości Fizyczne i Psychosomatyczne** — Spinal correction, neck/back pain. Methods: Dorn-Breuss, Cupping, Sound Bowl, Honey Massage, Trigger Point, Body Drum Release.

3. **Diagnostyka GDV i VedaPulse** — GDV Camera (Kirlian/Korotkov) aura reading + VedaPulse digital pulse diagnostics (Sorokin).

4. **The Reconnection i Reconnective Healing** — Eric Pearl method. The Reconnection: €333 (2 sessions, one-time). Reconnective Healing: multiple sessions.

---

## Testimonials

28 testimonials in the carousel. First/featured: **Czarek Głuch / Trader21** (with circular photo). Sources: `REFERENCES.doc` and `References ADDITION.doc` from Tamara.

---

## Contact Information

- **Email:** tamara@bodymindhealing.nl
- **WhatsApp:** +31 6 41450762
- **Address:** Blekerstraat 119, 1315 AD Almere, The Netherlands
- **Old website:** bodymindhealing.nl (hosted on VDX server 91.142.254.97)

---

## Design Process

1. Visual identity concepts created (3 directions)
2. Tamara chose "Warm & Spiritual" direction
3. Ideogram prompts generated → assets created in Ideogram
4. 3 landing page mockups built (Design A, B, C)
5. Tamara chose **Design C** ("Pełne Zanurzenie")
6. Full site built with subpages, gallery, legal pages
7. Deployed to GitHub Pages with custom domain
