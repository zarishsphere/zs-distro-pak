# PRD-MVP — `zs-distro-pak`

> **Document:** Product Requirements (MVP) | **Version:** 1.0.0-mvp
> **Repository:** [https://github.com/zarishsphere/zs-distro-pak](https://github.com/zarishsphere/zs-distro-pak)
> **Layer:** Layer 8 — Distribution | **Catalog #:** 188
> **Language:** YAML / JSON / Markdown | **License:** Apache 2.0

---

## Executive Summary

**Pakistan distro — provincial health codes, Urdu locale.**

This document defines the **Minimum Viable Product (MVP)** scope for `zs-distro-pak` within the ZarishSphere sovereign digital health platform. It covers what must be built first, acceptance criteria, user stories, and the complete repository file structure.


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

A country program cannot adopt ZarishSphere without a distribution layer that inherits global defaults and overrides them with country-specific forms, codes, terminology, and infrastructure configuration.

## MVP Goals

1. `distro.yaml` declares all overrides from `zs-distro-core`
2. Country-specific forms override global equivalents
3. National terminology code mappings provided for key systems
4. Facility registry seed file included
5. CI validates all YAML/JSON files

## Country-Specific Requirements

- Urdu (UR) full UI translation
- Provincial health authority code mappings
- NADRA national ID integration config
- EPI schedule for Pakistan

## MVP Functional Requirements

| ID | Requirement | Acceptance Criteria | Priority |
|----|------------|---------------------|---------|
| M-01 | distro.yaml valid YAML with required fields | `yamllint` passes | P0 |
| M-02 | All form overrides validate against ZS Form Schema v1 | Validation CI passes | P0 |
| M-03 | Facility registry contains real FHIR Location resources | JSON validates as FHIR Bundle | P1 |
| M-04 | Primary country language translation file present | lang/pak.json exists | P1 |
| M-05 | DHIS2 metadata config for national HMIS | dhis2/config.yaml present | P2 |

## MVP Complete Repository Tree

```
zs-distro-pak/
├── README.md                              # Country setup guide
├── LICENSE
├── distro.yaml                            # Distro manifest
├── .gitignore
├── CHANGELOG.md
├── .github/
│   ├── CODEOWNERS
│   └── workflows/
│       └── validate.yml
├── config/
│   ├── forms/
│   │   └── pak/                          # Pakistan-specific form overrides
│   │       └── (override JSON files)
│   ├── terminology/
│   │   └── pak-code-mappings.json        # National code ↔ FHIR mappings
│   ├── indicators/
│   │   └── pak-kpi-definitions.json      # Country KPI definitions
│   └── dhis2/
│       └── config.yaml                    # DHIS2 metadata configuration
├── translations/
│   └── pak.json                          # Primary country language
├── facilities/
│   └── facility-registry.json             # FHIR Bundle of Location resources
└── docs/
    ├── SETUP.md
    └── INDICATORS.md
```

## Configuration Inheritance

```
zs-distro-core  (global defaults, base FHIR profiles, core forms)
    └── zs-distro-pak  (Pakistan overrides — additive only, no deletions)
            └── zs-infra-pak/  (live infrastructure state)
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

*This document is the authoritative MVP specification for `zs-distro-pak`.*
*Changes require a Pull Request with at least 1 owner approval.*
