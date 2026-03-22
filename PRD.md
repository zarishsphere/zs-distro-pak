# PRD — `zs-distro-pak`

> **Document Class:** PRD | **Version:** 1.0.0 | **Status:** Bootstrapping
> **Repository:** [https://github.com/zarishsphere/zs-distro-pak](https://github.com/zarishsphere/zs-distro-pak)
> **Layer:** Layer 8 — Distribution | **Catalog #:** 188
> **License:** Apache 2.0 | **Governance:** RFC-0001

---

## 1. Overview

Pakistan distro — PKI integration, Urdu forms, provincial health authority codes.

---

## 2. Repository Metadata

- **Name:** `zs-distro-pak`
- **Organization:** [https://github.com/zarishsphere](https://github.com/zarishsphere)
- **Language / Runtime:** YAML / JSON / Markdown
- **Visibility:** Public
- **License:** Apache 2.0
- **Default Branch:** `main`
- **Branch Protection:** Required (2-owner review for critical paths)

---

## 3. Platform Context

This repository is part of the **ZarishSphere** sovereign digital health operating platform — a free, open-source, FHIR R5-native system for South and Southeast Asia.

**Non-negotiable constraints:**
- Zero cost — all tooling must use genuinely free tiers
- FHIR R5 native — all clinical data modelled as FHIR R5 resources
- Offline-first — must work without network connectivity
- No-coder friendly — GUI-first, template-driven
- Documentation as Code — all decisions in GitHub

---

## 4. Goals & Objectives

- Provide Pakistan configuration layer inheriting from zs-distro-core
- Override global defaults with country/program-specific forms, codes, and indicators
- Enable one-click country environment provisioning

## 5. Functional Requirements

| ID | Requirement | Priority |
|----|------------|---------|
| F-01 | Inherits all core forms from zs-distro-core | P0 |
| F-02 | Country-specific form overrides and additions | P0 |
| F-03 | National terminology code mappings | P0 |
| F-04 | DHIS2 metadata configuration for national HMIS | P1 |
| F-05 | Country-specific indicator definitions | P1 |
| F-06 | Language packs (primary country language) | P1 |
| F-07 | Facility registry seed data | P2 |

## 6. Repository Tree

```
zs-distro-pak/
├── README.md
├── LICENSE
├── distro.yaml                        # Distro manifest (inherits from core)
├── .gitignore
├── .github/
│   ├── CODEOWNERS
│   └── workflows/
│       └── validate.yml               # Validate distro config
├── config/
│   ├── forms/
│   │   └── (country-specific form overrides)
│   ├── terminology/
│   │   └── (national code system mappings)
│   ├── indicators/
│   │   └── (country KPI definitions)
│   └── dhis2/
│       └── (DHIS2 metadata config)
├── translations/
│   ├── (country language JSON files)
├── facilities/
│   └── facility-registry.json         # FHIR Location resources
└── docs/
    ├── SETUP.md                       # Country setup guide
    └── INDICATORS.md                  # Country indicator reference
```

## 7. Configuration Inheritance

```
zs-distro-core  (global defaults)
    └── zs-distro-pak  (country overrides)
            └── zs-infra-pak/  (site instances)
```

## 9. Ownership & Governance

| Role | GitHub User |
|------|-------------|
| Platform Lead | `@arwa-zarish` |
| Technical Lead | `@code-and-brain` |
| DevOps Lead | `@DevOps-Ariful-Islam` |
| Health Programs | `@BGD-Health-Program` |

All changes go through Pull Request → 1+ owner review → CI pass → merge.
Breaking changes require RFC + ADR.

---

## 10. Definition of Done

- [ ] All listed files exist with content
- [ ] CI pipeline passes (test + lint + security)
- [ ] README.md reflects current state
- [ ] OpenAPI / AsyncAPI spec present (services only)
- [ ] At least 1 integration test using testcontainers-go (Go) or Playwright (UI)
- [ ] No secrets committed (GitGuardian verified)
- [ ] CODEOWNERS file present
- [ ] Linked to CATALOGS.md and TODO.md

---

*This PRD is the canonical source of truth for this repository's purpose, structure, and requirements.*
*Changes require a PR against this file with owner approval.*
