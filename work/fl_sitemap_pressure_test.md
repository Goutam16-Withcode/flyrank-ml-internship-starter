# AI Fluency — Portfolio Sitemap Sketch & Pressure-Test Audit

- **Author:** Goutam (FlyRank Intern)
- **Track:** AI Fluency — Sitemap Design & Prompt Pressure-Test Audit
- **Date:** 2026-08-20

---

## 1. Portfolio Sitemap Sketch (The 4-Page Path)

```text
[Landing / Hero Page]  --->  [Case Studies / Work]  --->  [About / Proof]  --->  [Contact / Action]
  (Claim Statement)           (3 Production Demos)        (Background)           (Direct Contact Form)
```

### Sitemap Structure & Page Roles

| Page | Core Role | User Action Supported | Excluded Elements |
|---|---|---|---|
| **1. Landing / Hero Page** | State the primary value proposition & claim ("Applied ML for Search Intelligence"). | Direct visitor to review Capstone Case Studies. | No pop-ups, no generic testimonials, no unnecessary fluff. |
| **2. Case Studies / Work** | Present 3 validated production projects (FlyRank Search Decay Model, Data Contract Validator, Ranking Pipeline). | Prove technical rigor & Precision@50 lift results. | No unexecuted draft code or dummy mockups. |
| **3. About / Background** | Technical bio, core tool stack (Python, scikit-learn, SQL, DuckDB), and engineering philosophy. | Establish credibility and domain competence. | Excluded personal non-technical hobbies. |
| **4. Contact / Action** | Single primary call-to-action (Email, GitHub, LinkedIn links, Calendly form). | Direct recruiter/client outreach. | Excluded complex multi-field survey forms. |

---

## 2. Claude Project Configuration & Custom Instructions

- **Project Name**: `FlyRank ML Portfolio Build`
- **Custom Instructions (System Prompt)**:
  ```text
  You are an expert AI tutor and senior ML engineering reviewer. 
  
  User Persona: Goutam, a Machine Learning Intern at FlyRank developing applied search intelligence models.
  Proof Statement: "I build reproducible ML systems that detect search performance decay across 30k+ pages, delivering a 3.08x precision lift over hand-written rules."
  
  Guidance:
  - Act as a rigorous tutor who pressure-tests technical claims and web sitemaps.
  - Challenge weak UX assumptions, unverified claims, or bloated page structures.
  - Keep recommendations concise, actionable, and focused on decision-support metrics.
  ```

---

## 3. Pressure-Test Prompt & Output Log

### The Pressure-Test Prompt
> *"Act as a senior tech lead and UX auditor. Review my 4-page portfolio sitemap (Landing, Case Studies, About, Contact) against my proof statement: 'I build reproducible ML systems that detect search performance decay across 30k+ pages, delivering a 3.08x precision lift over hand-written rules.' Does every page directly support visitor conversion to my main action (contacting me for ML roles)? Where is the friction or fluff?"*

### Claude Output Response (Summary)
> 1. **Strengths**: The 4-page scope is tight and avoids unnecessary pages. The proof statement on the hero page sets clear expectation.
> 2. **Identified Friction Points**:
>    - *Friction A*: Forcing visitors to navigate to a separate "Contact" page adds an extra click. Put a primary CTA directly in the header and hero footer.
>    - *Friction B*: The "About" page risks becoming generic if separated from project achievements. Embed technical credentials directly alongside the Case Studies.
> 3. **Actionable Recommendation**: Add a direct "View Capstone Paper" CTA right inside the Hero banner.

---

## 4. Key Change Made Based on Pressure-Test

- **Sitemap Modification**: Added a direct secondary Call-To-Action (`[Read Capstone Paper]`) inside the **Hero Page**, allowing technical reviewers to jump directly to code/results without having to click through two intermediate navigation steps.
