# Serrano Lab Mentoring & Training Platform

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC_BY_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

**A structured, open-source mentoring tool for academic research labs — designed with NIH training plan requirements in mind.**

Built for the [Serrano Laboratory](https://serranolab.github.io/online/#home) at Boston University's Chobanian & Avedisian School of Medicine, Center for Regenerative Medicine (CReM).

---

## Overview

The Serrano Lab Mentoring & Training Platform provides complementary interfaces for **mentees** and **mentors/PIs** to track professional development, manage goals, record credentials, and generate documentation for fellowship applications, grants, and annual reviews.

It runs entirely in the browser as a single `index.html` file — no server, no database, no installation required. All data persists in the browser's `localStorage`.

### Why this exists

Standard IDP (Individual Development Plan) tools are often static PDFs or disconnected spreadsheets. This platform bridges the gap between what NIH expects in training plans (structured competencies, measurable milestones, documented mentoring) and what mentors and trainees actually need day-to-day: a living document that tracks progress, surfaces gaps, and generates exportable summaries on demand.

The mentor side is deliberately framed around **lab investment needs** rather than trainee comparison — a pedagogical choice to support growth-oriented mentoring culture.

---

## Features

### Mentee Portal

| Tab | Features |
|-----|----------|
| **Plan & Goals** | IDP profile (name, level, dates, career goal statement), SMART goals with drag-and-drop reordering, DAC & milestone scheduler (PhD/MD-PhD: committee meetings, qualifying exams, defense dates, F31/F32 deadlines) |
| **Track Progress** | Dashboard with overall stats and radar/spider chart, training competency matrix across 7 domains and 50+ skills organized by accordion sections, per-row progress bars |
| **Professional Record** | Certificate tracker with PDF upload, publication & manuscript pipeline (Idea → Published with stage badges), conference & presentation log, teaching & outreach hours |
| **Meeting Log** | 1:1 mentor meeting tracker with discussion notes and rolling action items — uncompleted items carry forward to the next meeting |
| **Networking** | Contact tracker with organization, event, follow-up status, and aggregate stats |
| **Career Timeline** | Interactive timeline builder for F-series fellowships and grant figures — customizable year columns, editable row categories (goals, effort allocation bars, activities, seminars, conferences), auto-totaling effort percentages, text and print/PDF export |
| **Export** | CSV (compatible with mentor import), Print/PDF, IDP summary text, CV components export, career timeline export, Formspree email submission |

### Mentor / PI Portal

| Tab | Features |
|-----|----------|
| **Lab Health** | CSV import (drag-and-drop, accumulates across uploads), aggregate lab statistics, radar chart of lab-wide training coverage, trainee cards with progress bars, training coverage heatmap |
| **Individual Growth** | Per-trainee deep dive with stats, radar chart, area breakdown, and skill table; mentor-defined goals per trainee with status tracking |
| **Mentoring Reflection** | Auto-generated insights from trainee data (blocked items, lowest coverage areas), four structured self-reflection prompts, mentor action item tracker |
| **Reference Builder** | Generates draft paragraphs for recommendation letters, training plans, annual reviews (BUGWU), and grant progress reports — auto-populated from trainee data, PI notes, and mentor goals |
| **Export** | Group CSV (all trainees), PI notes and goals as JSON (import/export), print/PDF |

### General

- **Persistent storage** via `localStorage` — data survives browser refresh and session changes
- **High-contrast mode** for accessibility
- **Print-optimized CSS** for PDF generation
- **Responsive layout** for mobile and tablet
- **SVG icon system** (no external icon dependencies)
- **Single-file deployment** — one HTML file, no build step

---

## Training Competency Framework

The platform includes a structured competency taxonomy across **7 domains**, tailored by trainee level (Undergraduate, PhD, MD/PhD, Post-doc, Staff):

1. **Core Lab Practices** — Safety, responsible conduct, data stewardship, FAIR principles, EDIA, team communication, patient engagement
2. **Personal & Professional Development** — IDP planning, career growth, grant writing, leadership, mentoring
3. **Technical & Research Skills** — Cell biology, iPSC, zebrafish, flow cytometry, computational biology, single-cell RNAseq
4. **Scientific Communication & Engagement** — Presentations, non-scientific audiences, advocacy, open science tools
5. **Academic & Clinical Training** — Coursework, GCP certification, clinical exposure, seminars
6. **Progress Monitoring & Feedback** — 1:1 meetings, committee meetings, self-assessment
7. **Laboratory Operations & Staff Development** — Instrumentation, regulatory compliance, SOPs, purchasing, coordination

Each skill is level-gated so trainees see only what's relevant to their career stage.

---

## Quick Start

### Option 1: Direct use

1. Download `index.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. Start filling in the Mentee or Mentor portal

### Option 2: GitHub Pages

1. Fork or clone this repository
2. Enable GitHub Pages (Settings → Pages → Source: `main` branch, root `/`)
3. Access at `https://ma-serr.github.io/mentoring-platform/`

### Option 3: Custom domain

Host `index.html` on any static hosting (Netlify, Vercel, DigitalOcean, your own server). No backend required.

---

## Workflow

```
┌─────────────┐         CSV export          ┌─────────────────┐
│   MENTEE    │ ──────────────────────────▶  │   MENTOR / PI   │
│   Portal    │                              │   Portal        │
│             │  ◀──── Goals & feedback ──── │                 │
│ • IDP setup │         (in person)          │ • Import CSVs   │
│ • Goals     │                              │ • Set goals     │
│ • Matrix    │                              │ • Write notes   │
│ • Certs     │                              │ • Build refs    │
│ • Meetings  │                              │ • Reflect       │
│ • Network   │                              │ • Export        │
└─────────────┘                              └─────────────────┘
```

1. **Mentee** fills in their profile, sets goals, works through the training matrix over time
2. **Mentee** exports CSV periodically and sends to mentor (via download or Formspree)
3. **Mentor** imports trainee CSVs into the PI portal (multiple trainees accumulate)
4. **Mentor** reviews progress, sets mentor-defined goals, writes PI notes
5. **Mentor** uses Reference Builder to generate paragraphs for letters, reviews, reports
6. **Mentor** uses Mentoring Reflection tab for self-assessment and action planning
7. Repeat as training progresses

---

## Data & Privacy

- **All data stays in your browser.** Nothing is sent to any server (except optional Formspree email submission, which the mentee initiates manually).
- Data is stored in `localStorage` under keys prefixed with `serrano_mentee_v22` and `serrano_pi_v22`.
- Certificate PDF uploads are stored as base64 in localStorage (max 2 MB per file).
- Clearing browser data or using incognito mode will reset all data.
- PI notes and mentor goals can be exported as JSON for backup and imported on any browser.

---

## Customization

### Adapting the competency framework

The training areas are defined in the `MA` array near the top of the `<script>` block. Each entry follows this structure:

```javascript
{
  group: "Domain Name",
  topics: [
    {
      topic: "Topic Name",
      skills: [
        { name: "Skill Name", level: ["ug", "phd", "md/phd", "postdoc", "staff"] }
      ]
    }
  ]
}
```

To adapt for your lab, edit the `MA` array directly in the HTML file. Add or remove skills, topics, and domains as needed. Update the `RADAR_SHORT` label map if you change domain names.

### Changing the Formspree endpoint

Replace the form action URL in the hidden `<form id="matrixForm">` element with your own Formspree (or other form handler) endpoint.

### Branding

Edit the topbar HTML and CSS variables in `:root` to match your lab's colors and name.

---

## Browser Support

Tested on:
- Chrome 120+
- Firefox 120+
- Safari 17+
- Edge 120+

Requires JavaScript enabled. Uses ES6+ features (template literals, arrow functions, destructuring, `localStorage`).

---

## Contributing

Contributions are welcome. If adapting for your own lab:

1. Fork the repository
2. Modify the competency framework in the `MA` array
3. Update branding in the CSS and topbar
4. Submit a pull request if you build features that would benefit the community

For bug reports or feature requests, please open an issue.

---

## Credits

| Contributor | Role | Contributions |
|-------------|------|---------------|
| **Dr. Maria A. Serrano** | Creator & Content Author | Conceptual design, training framework architecture (7 domains, 50+ skills), competency taxonomy, mentoring pedagogy, IDP/NIH/DAC alignment requirements, reflection prompts, all domain content, pedagogical direction (growth-centered vs. comparison framing) |
| **Claude (Anthropic)** | Development Partner | UI/UX design, front-end implementation (HTML/CSS/JS), data architecture, CSV pipeline, radar chart visualization, reference paragraph builder, localStorage persistence, networking tracker, publication pipeline, 1:1 meeting log, DAC milestone scheduler, teaching tracker, CV components export, accessibility features |

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| **v1.0** | 2025 | Separate Mentee Training Matrix and PI Progress Dashboard with CSV exchange |
| **v2.0** | 2026 | Unified platform with IDP builder, SMART goals, certificate tracker, reference paragraph builder |
| **v2.1** | 2026 | Pedagogical redesign (removed comparison framing, added Mentoring Reflection), radar charts, drag-and-drop goals, certificate PDF uploads, SVG icon system, Source Sans 3 typography |
| **v2.2** | 2026 | Sub-tab navigation, DAC milestone scheduler, publication pipeline, conference log, 1:1 meeting log with rolling action items, networking tracker, teaching & outreach hours, CV components export |
| **v2.3** | 2026 | Career Timeline Builder for F-series fellowships and grant applications — customizable year columns, effort allocation bars, editable activity rows, auto-totaling, text export |

---

## License

This project is licensed under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt this work for any purpose, including commercially, as long as you provide appropriate attribution. See [LICENSE](LICENSE) for details.

---

## Citation

If you use this platform in a publication or grant application:

> Serrano, M.A. & Claude (Anthropic). *Serrano Lab Mentoring & Training Platform* (v2.3). Boston University Center for Regenerative Medicine. 2026. Available at: https://github.com/ma-serr/mentoring-platform

---

## Contact

**Dr. Maria A. Serrano**
Assistant Professor of Medicine
Center for Regenerative Medicine (CReM)
Boston University Chobanian & Avedisian School of Medicine
[serranolab.org](https://serranolab.github.io/online/#home)
