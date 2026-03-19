<div align="center">

# LitAssist

**Platform otomasi riset literatur akademik untuk mahasiswa skripsi & peneliti**

[![Made with Node.js](https://img.shields.io/badge/Node.js-20-339933?style=flat-square&logo=nodedotjs&logoColor=white)](https://nodejs.org)
[![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![MongoDB](https://img.shields.io/badge/MongoDB-6-47A248?style=flat-square&logo=mongodb&logoColor=white)](https://mongodb.com)
[![Alpine.js](https://img.shields.io/badge/Alpine.js-3-77C1D2?style=flat-square&logo=alpine.js&logoColor=white)](https://alpinejs.dev)
[![License](https://img.shields.io/badge/License-Private-red?style=flat-square)](.)

[Features](#-features) · [Screenshots](#-screenshots) · [Architecture](#️-architecture) · [Tech Stack](#-tech-stack) · [Security](#-security) · [Contact](#-contact)

</div>

---

## What is LitAssist?

LitAssist is a full-stack web application that automates the academic literature review process. Instead of manually searching across multiple databases, downloading papers one by one, and organizing them in spreadsheets — LitAssist does it all in one click.

**Built for:** Indonesian thesis students and academic researchers who need to collect and manage journal references efficiently.

---

## Features

| Feature | Free | Premium |
|---|---|---|
| Auto-scraping (Google Scholar, Scopus, Semantic Scholar) | ✔ | ✔ |
| Personal journal library | ✔ | ✔ |
| Journal statistics & analytics | ✔ | ✔ |
| Search, filter, sort | ✔ | ✔ |
| Lifetime journal quota | 10 | Unlimited |
| Scrapes per day | 2 | Unlimited |
| Max target per scrape | 25 | 50 |
| AI Literature Review (Gemini) | ✘  | ✔ |
| Export Excel & BibTeX | ✘  | ✔ |
| Queue priority | Standard | Priority |

---

## Screenshots

### Landing Page
![Landing Page](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/landing-hero.png)

### Journals Dashboard
![Journals Dashboard](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/dashboard.png)

### Personal Library
![Library](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/library.png)

### AI Summary (Premium)
![AI Summary](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/ai-summary.png)

### Statistics & Analytics
![Stats](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/stats.png)

### Pricing
![Pricing](https://raw.githubusercontent.com/ridhoajaaa/litassist/main/assets/pricing.png)

---

## Architecture

```
User clicks "Start Scrape"
        │
        ▼
  Socket.IO event ──→ scraper/index.js (Node.js + Puppeteer)
        │
        ├── Google Scholar  (Puppeteer + Chromium)
        ├── Scopus          (Semantic Scholar API)
        └── Semantic Scholar (API direct)
        │
        ▼
  jurnal_mentah.json (raw output)
        │
        ▼
  processor/main.py (Python + Pandas)
  ├── Clean & normalize metadata
  ├── Detect & remove duplicates
  ├── Classify into research categories
  └── Calculate relevance scores
        │
        ▼
  MongoDB (bulk insertMany)
        │
        ▼
  Dashboard updates via Socket.IO (real-time)
```

### CAPTCHA Handling

Google Scholar aggressively blocks scrapers with CAPTCHA. LitAssist solves this with an embedded **noVNC** panel:

1. Scraper detects CAPTCHA → pauses automatically
2. Socket.IO notifies the frontend
3. noVNC panel appears in the dashboard
4. User solves CAPTCHA visually in the browser
5. Scraper resumes automatically

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Alpine.js 3, Tailwind CSS 4, MPA |
| **Backend** | Node.js 20, Express 5, Socket.IO 4 |
| **Database** | MongoDB 6, Mongoose |
| **Scraping** | Puppeteer, Chromium, Semantic Scholar API |
| **AI** | Google Gemini 2.5 Flash |
| **Data Processing** | Python 3, Pandas |
| **Infrastructure** | Podman, Docker Compose |
| **Tunnel** | ngrok |

---

## Security

LitAssist has been through a full security audit:

```
ZAP Baseline Scan:    0 FAIL  · 7 WARN (all CDN trade-offs)  ✔
npm audit:            0 vulnerabilities                        ✔
Nikto:                0 critical findings                      ✔
Trivy (deps):         0 CVEs                                   ✔
```

Security measures implemented:
- **Helmet.js** — full HTTP security header suite
- **CSP** — Content Security Policy with strict directives
- **Rate limiting** — auth endpoints: max 20 req/15min (99.98% brute force blocked in load test)
- **bcrypt** — password hashing
- **express-session** + MongoDB session store
- **ETag disabled** — prevents inode information leak
- **gzip compression** — all responses compressed

---

## Performance (Lighthouse Mobile)

| Category | Score |
|---|---|
| Performance | 87 |
| Accessibility | 93 |
| Best Practices | 100 |
| SEO | 100 |

---

## Load Testing (k6)

| Scenario | Users | Requests | Error Rate | Avg Response |
|---|---|---|---|---|
| Static pages | 100 | 7,493 | 0% | 6.78ms |
| Full user journey | 10 | 1,665 | 0% | 6ms |
| Rate limiter stress | 25 | 161,004 | 0% crash | 4.61ms |
| API endpoints | 20 | 3,668 | 0% | 4ms |

---

## Roadmap

- [ ] Deploy to production (VPS)
- [ ] Zotero integration
- [ ] PubMed & IEEE Xplore support
- [ ] Batch processing for multiple topics
- [ ] Mobile-optimized PWA

---

## Contact

**Interested in using LitAssist or collaborating?**

- Email: [alfariziridha014@gmail.com]
- Instagram: [@idhoaf_]
- LinkedIn: [Muhammad-Ridha-Alfarizi]

> **Note:** Source code is currently private. Contact me if you're interested in a demo or collaboration.

---

<div align="center">

*Node.js · Python · Alpine.js · Tailwind CSS · MongoDB · Socket.IO · Puppeteer*

</div>