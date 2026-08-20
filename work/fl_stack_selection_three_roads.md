# AI Fluency — Three Roads: Stack Trade-Off Audit & Selection Rationale

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — Week 4 Tech Stack Trade-Off Analysis (`Three Roads`)
- **Date:** 2026-08-20

---

## 1. The Four Core Constraints

1. **Budget Constraint**: **100% Free Only** (Zero hosting, domain, or API infrastructure costs).
2. **Skill Level Alignment**: Experienced in Python, Data Science, SQL, and clean Vanilla HTML5/CSS/JS; preferring low maintenance over complex web frameworks.
3. **Portfolio Requirements**: Must render long-form Markdown technical reports (`capstone_report.md`), embed SVG data visualizations, showcase terminal stdout receipts, and display GitHub code links.
4. **Backend Necessity**: **Not needed yet**. The current portfolio displays static empirical research receipts; a dynamic database backend is unnecessary for Phase 1.

---

## 2. Evaluation of Three Stack Options (Simplest to Most Powerful)

| Criteria | Option A: HTML5 / GFM / GitHub Pages *(Simplest)* | Option B: Vite + React SPA / Netlify *(Intermediate)* | Option C: Next.js + Serverless / Vercel *(Most Powerful)* |
|---|---|---|---|
| **Build Method** | Static HTML5 + GitHub Flavored Markdown renderer. | React component-based single-page application. | Next.js App Router with Server-Side Rendering (SSR). |
| **Hosting (Free)** | **GitHub Pages** (Built into repo, 100% free forever). | Netlify / Vercel Free Tier. | Vercel Free Tier. |
| **Backend Required?** | **No** (Pure static rendering). | No (Client-side rendering). | Optional (API routes available). |
| **Build Time** | **< 1 Day** (Zero build pipeline overhead). | ~ 3–5 Days (Component setup & package management). | ~ 1–2 Weeks (Complex routing & SSR setup). |
| **Trade-Off** | Lacks interactive React component state transitions. | Requires Node.js dependency updates over time. | High maintenance overhead; risk of serverless cold starts. |

---

## 3. Pressure-Test Audit

- **What breaks if I pick Option A (Simplest)?**: Nothing breaks for research presentation. GitHub Pages renders Markdown reports natively with instant load times and zero build failures.
- **What do I maintain if I pick Option C (Most Powerful)?**: Maintaining Next.js framework upgrades, npm package vulnerabilities, and Vercel deployment configs adds friction that distracts from ML research work.
- **Can I finish in two weeks?**: Option A takes <1 day, guaranteeing on-time submission without build blockers.
- **Does it display my work well?**: Yes. Long-form Markdown rendering is the native standard for research papers and technical documentation.

---

## 4. Final Written Rationale & Decision

> **Chosen Stack**: **Option A — HTML5 & GitHub Flavored Markdown (GFM) hosted on GitHub Pages.**
> 
> **Why I Chose Option A**: 
> 1. *Can I maintain this?*: Yes, effortlessly. There are zero npm dependencies or framework updates to manage; committing a `.md` file automatically updates the live page.
> 2. *Does it show my work well?*: Yes. My primary proof consists of technical research reports, data tables, and Python code blocks. Markdown is the industry-standard format for data science and ML engineering portfolios.
> 3. *Why I rejected Options B & C*: React and Next.js introduce build setup overhead and bundle bloat without adding value to static empirical research papers. "Not yet" is the honest answer for backend requirements—Option A delivers maximum stability with zero maintenance friction.
