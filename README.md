# Vendor Security Risk Assessment Tool

**Live Demo:** [vendor-risk-assessment.pages.dev](https://vendor-risk-assessment.pages.dev)  
**Built by:** [Chris Olowo, PMP®](https://chris-olowo-grc-portfolio.pages.dev) — GRC Analyst & Risk Practitioner

---

## Overview

A fully interactive, browser-based third-party vendor security risk assessment tool that evaluates supplier security posture across **6 domains** and **29 weighted questions**, mapped to ISO 27001:2022 controls, NIST CSF 2.0 functions, SOC 2 Trust Service Criteria, GDPR Article 28, and PIPEDA.

Generates a **risk-rated report** (Critical / High / Medium / Low) with domain breakdowns, detailed findings, recommended risk treatments, and control references. All data is stored locally in the browser — nothing leaves your device.

---

## Features

- **6 Security Assessment Domains**
  - Data Security & Privacy
  - Access Controls & Identity Management
  - Incident Response & Recovery
  - Business Continuity & Availability
  - Compliance & Regulatory
  - Third-Party Sub-processors & Supply Chain

- **29 Weighted Questions** — each mapped to specific framework controls
- **Automated Risk Scoring Engine** — weighted scoring with risk thresholds
- **Risk Rating** — Critical / High / Medium / Low with narrative summary
- **Domain Breakdown** — per-domain risk scores with visual progress bars
- **Detailed Findings Table** — every answer with framework control references
- **Recommended Risk Treatments** — prioritized gap list with severity ratings
- **Assessment History** — saved to localStorage, loadable and deletable
- **Export to JSON** — full assessment data export
- **Print / Save PDF** — print-optimized layout
- **Light / Dark Mode** — persisted via localStorage
- **Fully Responsive** — works on desktop and mobile

---

## Framework Coverage

| Framework | Controls Referenced |
|---|---|
| ISO 27001:2022 | A.5.1, A.5.12, A.5.15, A.5.19, A.5.20, A.5.26, A.5.27, A.5.29, A.5.30, A.5.34, A.5.36, A.6.3, A.6.5, A.8.2, A.8.5, A.8.8, A.8.10, A.8.13, A.8.14, A.8.15, A.8.24, A.8.30 |
| NIST CSF 2.0 | GV.OC-05, GV.PO-01, ID.AM-05, ID.RA-01, ID.RA-05, ID.SC-02, ID.SC-03, ID.SC-04, PR.AC-01, PR.AC-04, PR.AC-05, PR.AC-07, PR.AT-01, PR.DS-01, PR.DS-02, PR.DS-03, PR.DS-04, PR.DS-06, RS.AN-02, RS.RP-01, RC.RP-01 |
| SOC 2 Type II | CC1.3, CC1.4, CC6.1, CC6.2, CC6.3, CC6.5, CC6.7, CC7.1, CC7.3, CC7.4, CC9.2, A1.1, A1.2, A1.3 |
| GDPR | Art. 25, Art. 28, Art. 28(2), Art. 33 |
| PIPEDA | Principle 4, Breach Notification Regulations |

---

## Security Architecture

All security headers are enforced server-side via the Cloudflare `_headers` file:

| Header | Value |
|---|---|
| `X-Frame-Options` | `DENY` |
| `X-Content-Type-Options` | `nosniff` |
| `Referrer-Policy` | `strict-origin-when-cross-origin` |
| `Strict-Transport-Security` | `max-age=63072000; includeSubDomains; preload` |
| `Content-Security-Policy` | Strict allowlist — no inline eval, no external data exfiltration |
| `Permissions-Policy` | Geolocation, microphone, camera, payment all denied |
| `X-XSS-Protection` | `1; mode=block` |

**Additional security controls:**
- HTTPS enforcement via JavaScript (redirects HTTP → HTTPS, excludes localhost)
- GitHub Pages → Cloudflare Pages redirect (canonical URL enforcement)
- Chart.js loaded with **Subresource Integrity (SRI)** hash + `crossorigin="anonymous"` + `referrerpolicy="no-referrer"`
- Chart.js safety stub IIFE — prevents app crash if CDN is unavailable
- `localStorage` wrapped in `try/catch` — graceful degradation if storage is denied
- `prefers-reduced-motion` media query — accessibility compliance
- Passive scroll event listeners throughout
- Deep-link hash validation against explicit allowlist
- All user input HTML-escaped before DOM insertion (XSS prevention)
- No cookies, no tracking, no third-party analytics
- All data stored exclusively in `localStorage` — no server-side data collection

**ISO 27001 control mapping for this application's own architecture:**

| Current State | Target / Roadmap | Control Reference |
|---|---|---|
| Static hosting + CDN | WAF, runtime protection, IDS | A.8.20–22 · NIST PR.AC |
| No authentication | Identity provider (Okta / Entra ID) with MFA and RBAC | A.5.15–18 · NIST PR.AC-01 |
| SRI on CDN scripts | Software composition analysis (Snyk) + verified build pipeline | A.12.6 · NIST ID.SC-04 |

---

## Repository Structure

```
vendor-risk-assessment-tool/
├── index.html      ← Full application (single-file, no build step required)
├── _headers        ← Cloudflare Pages security headers
└── README.md       ← This file
```

---

## Running Locally

No build step or server required. Open directly in any modern browser:

```bash
git clone https://github.com/chrisolowolafe-sys/vendor-risk-assessment-tool.git
cd vendor-risk-assessment-tool
open index.html
```

---

## Deployment (Cloudflare Pages)

1. Fork or clone this repository
2. Connect to [Cloudflare Pages](https://pages.cloudflare.com)
3. Set build command: *(none — static site)*
4. Set output directory: `/` (root)
5. Deploy — the `_headers` file is automatically applied by Cloudflare

---

## Part of the GRC Portfolio

This tool is one of a series of standalone GRC projects:

| Project | Description |
|---|---|
| [ShomriTech GRC Platform](https://chris-olowo-grc-portfolio.pages.dev/grc-platform) | Enterprise GRC platform — 9 framework assessments, risk register, controls, evidence management |
| **Vendor Risk Assessment Tool** *(this repo)* | Third-party vendor security risk assessment |
| User Access Review Tracker | *(coming soon)* |
| SOC 2 Evidence Tracker | *(coming soon)* |
| NIST AI RMF Gap Assessment | *(coming soon)* |

---

## Author

**Chris Olowo, PMP®**  
GRC Analyst & Risk Practitioner · Calgary, Canada  
ISO 27001 Lead Auditor · NIST CSF 2.0 · GRC · PrivacyOps · ISO 42001

[Portfolio](https://chris-olowo-grc-portfolio.pages.dev) · [LinkedIn](https://www.linkedin.com/in/chris-o-742316135)

---

*For demonstration and educational purposes only. Not a certified compliance platform or legal service. Framework references are paraphrased for educational purposes.*
