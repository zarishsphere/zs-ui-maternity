# PRD-MVP — `zs-ui-maternity`

> **Document:** Product Requirements (MVP) | **Version:** 1.0.0-mvp
> **Repository:** [https://github.com/zarishsphere/zs-ui-maternity](https://github.com/zarishsphere/zs-ui-maternity)
> **Layer:** Layer 3 — Frontend MFEs | **Catalog #:** 97
> **Language:** TypeScript 5.8 / React 19 / Next.js 15.3 | **License:** Apache 2.0

---

## Executive Summary

**ANC/PNC care — partograph, birth registry.**

This document defines the **Minimum Viable Product (MVP)** scope for `zs-ui-maternity` within the ZarishSphere sovereign digital health platform. It covers what must be built first, acceptance criteria, user stories, and the complete repository file structure.


### Platform Non-Negotiables (apply to every repository)

| Constraint | Rule |
|-----------|------|
| **Zero Cost** | All tooling, hosting, and services must use genuinely free tiers |
| **Open Source** | Apache 2.0 license; all code public |
| **FHIR R5 Native** | All clinical data modelled as FHIR R5 resources |
| **Offline-First** | Must function without network connectivity |
| **No-Coder Friendly** | GUI-first, template-driven, automatable |
| **Documentation as Code** | All decisions in GitHub via RFC/ADR |
| **Multi-tenant** | tenant_id scoping on all data operations |
| **HIPAA/GDPR** | AuditEvent on all PHI access; field-level encryption |

---

## Problem Statement

ANC/PNC care — partograph, birth registry. is required for maternity workflows in the ZarishSphere platform.

## MVP Goals

1. Deliver a usable, accessible React microfrontend for maternity workflows
2. Integrate with FHIR R5 backend via zs-pkg-ui-fhir-hooks
3. Support offline operation via IndexedDB (Dexie.js)
4. Render in the shell application via Module Federation
5. Support EN and BN (Bengali) at minimum for MVP

## MVP User Stories

- As a user, I can use anc/pnc care — partograph, birth registry. through a clean, accessible interface.
- As a clinician, the interface works offline and syncs when connectivity returns.

## MVP Functional Requirements

| ID | Requirement | Acceptance Criteria | Priority |
|----|------------|---------------------|---------|
| M-01 | ANC/PNC care — partograph, birth registry. renders without error | Main component loads in browser | P0 |
| M-02 | FHIR data loads from backend | Data visible when backend is running | P0 |
| M-03 | EN + BN translations present | i18n works in both languages | P1 |
| M-04 | Offline fallback to IndexedDB | Data shown from cache when offline | P1 |

## Out of Scope for MVP

- All languages beyond EN + BN
- Dark mode
- Advanced analytics
- Print-optimized views
- Voice input

## MVP Complete Repository Tree

```
zs-ui-maternity/
├── README.md
├── LICENSE
├── package.json
├── tsconfig.json
├── vite.config.ts                         # Module Federation + React plugin
├── .eslintrc.json
├── vitest.config.ts
├── .gitignore
├── CHANGELOG.md
├── .github/
│   ├── CODEOWNERS
│   └── workflows/
│       └── ci.yml
├── src/
│   ├── main.tsx                           # Microfrontend bootstrap entry
│   ├── App.tsx                            # Root component
│   ├── bootstrap.tsx                      # Async import wrapper
│   ├── components/
│   │   ├── MaternityMain/
│   │   ├── │   │   │   └── MaternityMain.tsx
│   │   ├── │   │   ├── (feature sub-components)
│   ├── hooks/
│   │   ├── useMaternityData.ts  # FHIR data hook
│   │   └── useOfflineSync.ts              # Dexie.js sync hook
│   ├── pages/
│   │   ├── index.tsx                      # Main page
│   │   └── (feature pages)
│   ├── store/
│   │   └── maternityStore.ts                  # Zustand state slice
│   ├── types/
│   │   └── index.ts                       # TypeScript interfaces
│   ├── i18n/
│   │   ├── en.json                        # English strings
│   │   └── bn.json                        # Bengali strings
│   └── styles/
│       └── index.css
├── tests/
│   ├── unit/
│   │   └── components/
│   └── e2e/
│       └── maternity.spec.ts                  # Playwright E2E test
└── public/
    └── index.html

```

---


## Owners & Governance

| Role | GitHub Handle | Responsibility |
|------|--------------|----------------|
| Platform Lead | `@arwa-zarish` | Final approval, RFC votes |
| Technical Lead | `@code-and-brain` | Architecture, Go/TS review |
| DevOps Lead | `@DevOps-Ariful-Islam` | CI/CD, infra, deployment |
| Health Programs | `@BGD-Health-Program` | Clinical content, country programs |

**PR Policy:** All changes via Pull Request. Minimum 1 owner review. CI must pass. No direct commits to `main`.


---

## MVP Acceptance Checklist

- [ ] All MVP files exist in repository with real content (not placeholders)
- [ ] CI pipeline passes on `main` branch
- [ ] No secrets, credentials, or PHI committed
- [ ] README.md reflects current state with setup instructions
- [ ] CODEOWNERS file present
- [ ] All MVP functional requirements verified manually or via automated tests
- [ ] Linked to `CATALOGS.md` and `TODO.md` in `zs-docs-platform`

---

*This document is the authoritative MVP specification for `zs-ui-maternity`.*
*Changes require a Pull Request with at least 1 owner approval.*
