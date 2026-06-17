# BOOST Hub — Coaching Session Management App

Internal coaching tool for the Learning & Development team at **Dermorepubliq Corporation**.  
Manages coaching sessions, action plans, e-signatures, and progress tracking across coaches and coachees.

**Live app:** https://dermorepubliqld.github.io/coachingapp/

---

## What it does

- Coaches log sessions, set action plans, and track coachee progress
- Coachees view their sessions, submit reflections, and acknowledge completed coaching records
- Directors monitor compliance, coaching activity, and team-wide action plan health
- All session records export as a formatted PDF (HR-TMP-009-1.2-2025)
- E-signatures captured in-app and embedded in the PDF export

---

## Access & roles

| Role | What they can do |
|---|---|
| **Director** | Full access — dashboard, all sessions, user management, reports, settings |
| **Coach** | My Team, session form, action plans, PDF export |
| **Coachee** | My Coaching (sessions list), My Action Plans, acknowledgement flow |

Users can hold multiple roles (e.g. a coach who is also a coachee).  
New users are created by a Director in the User Management section.

---

## Tech stack

| Layer | Details |
|---|---|
| Frontend | Single HTML file — all JS and CSS inline, no build step |
| Auth | Firebase Authentication (email/password) |
| Database | Firebase Firestore |
| Email | EmailJS (optional, toggle in Settings) |
| Hosting | GitHub Pages (`index.html` served from repo root) |
| Fonts | Figtree (UI), Sora (headings) via Google Fonts |

**Firebase project:** `ldcoach-83aed`  
Firestore console: https://console.firebase.google.com/project/ldcoach-83aed

---

## File structure

```
Coaching App/
├── index.html              # GitHub Pages deploy copy — this is what the live site serves
├── ldcoach.html            # Development working file — edit this one
├── README.md               # This file
├── Logo.png                # Dermorepubliq logo (used in PDF header)
├── CoachingApp_TechBrief.docx   # Technical brief (13 sections)
├── Coaching Template.docx       # Original HR coaching form (HR-TMP-009-1.2-2025)
├── template_page-1.jpg          # Reference screenshot — PDF page 1
└── template_page-2.jpg          # Reference screenshot — PDF page 2
```

> **Always edit `ldcoach.html`, then copy to `index.html` before pushing.**  
> Never edit `index.html` directly.

---

## How to deploy

1. Make changes in `ldcoach.html`
2. Copy: `cp ldcoach.html index.html`
3. Commit and push both files to the `main` branch
4. GitHub Pages serves the updated app within ~1 minute

---

## Key Firestore collections

| Collection | Contents |
|---|---|
| `users` | User profiles, roles, e-signature (base64), coachId |
| `sessions` | Coaching session records (coachId, coacheeId, status, AP data) |
| `actionPlans` | Individual action plan items linked to sessions |
| `settings` | App-wide config (EmailJS toggle, etc.) |
| `meta/sessionCounter` | Auto-increment counter for session codes (CS-001, CS-002…) |

---

## Session lifecycle

```
Draft → Prep Requested → Coachee Preparing → Prep Submitted →
Coach Review → For Review → Pending Commitment →
Pending Acknowledgement → Acknowledged / Completed
```

Coach-Led sessions skip the prep steps and go directly to the session form.

---

## Maintainer

**Sandy Barlao** — Learning & Development Director, Dermorepubliq  
sbarlao@dermorepubliq.com
