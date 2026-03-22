# TECH-DESIGN-MVP — `zs-distro-pak`

> **Document:** Technical Design (MVP) | **Version:** 1.0.0-mvp
> **Repository:** [https://github.com/zarishsphere/zs-distro-pak](https://github.com/zarishsphere/zs-distro-pak)
> **Layer:** Layer 8 | **Catalog #:** 188
> **Language:** YAML / JSON | **License:** Apache 2.0

---

## Technical Summary

**Pakistan distro — provincial health codes, Urdu locale.**

This document defines the **technical architecture, implementation design, complete repository tree, and acceptance criteria** for the MVP of `zs-distro-pak`.

---

## distro.yaml Schema

```yaml
# zs-distro-pak/distro.yaml
apiVersion: zarishsphere.com/v1
kind: Distro
metadata:
  name: zs-distro-pak
  country: Pakistan
  countryCode: PAK
  language: pak
  version: 1.0.0
  
inherits:
  - zs-distro-core

overrides:
  forms:
    - source: config/forms/pak/
      replaces: forms/core/
  terminology:
    - file: config/terminology/pak-code-mappings.json
  indicators:
    - file: config/indicators/pak-kpi-definitions.json
      
features:
  dhis2: enabled
  abdm: disabled
  unhcr: disabled
  
languages:
  primary: pak
  supported: [en, pak]
```

## Validation CI

```yaml
name: Validate Distro
on: [push, pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: pip install yamllint jsonschema
      - run: yamllint distro.yaml config/
      - run: python scripts/validate_forms.py
      - run: python scripts/validate_facility_registry.py
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
