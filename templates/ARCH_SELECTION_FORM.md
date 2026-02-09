# Initial Architecture & Stack Selection Pass

**Goal:** Standardize the initial architectural choices for the project. 
**Instructions:** Review the recommended options below. They are pre-selected based on the "Gold Standard" for this use case. If you agree, leave as is. If you need to override, change the selection or use the "Free-form" section.

---

## 1. Project Context
*   **Project Name:** 
*   **Primary Goal:** [e.g., Local Tool, Public SaaS, Static Content]
*   **Scale Expectation:** [e.g., Small/Internal, Medium/Regional, Large/Global]

## 2. Frontend Strategy
*Select all that apply for different sub-domains.*

- [x] **Next.js (App Router):** Recommended for Public SaaS, SEO, and complex web apps.
- [ ] **Datastar / Gonads:** Recommended for real-time dashboards and hypermedia-driven UIs.
- [ ] **Vite + React:** Recommended for local developer tools and embedded admin panels.
- [ ] **Static Export:** Recommended for blogs and brochure sites (99/100 Lighthouse target).

**Frontend Overrides / Notes:**
> 

---

## 3. Backend & Persistence
*Select the primary pattern for the core domain.*

- [x] **Standard CRUD (SQLite/Postgres):** Recommended for most applications.
- [ ] **Event Sourcing:** Recommended for systems requiring high auditability or complex history.
- [ ] **CQRS:** Recommended for performance-divergent read/write requirements.

**Backend Overrides / Notes:**
> 

---

## 4. Local Development & Demo
- [x] **SQLite + Seeding:** Recommended for local dev and demo modes.
- [x] **Role Selection Page:** Recommended for skipping login in non-prod environments.

---

## 5. Free-form Architectural Decisions
*Use this section for decisions not covered above or for "Hybrid" architectural plans.*

> 

---

## 6. Real-time Clarity Check
*Are there any specific areas where you need more guidance or where the domain complexity is high?*

> 
