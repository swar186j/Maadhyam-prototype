# Maadhyam

**AI-powered citizen assistance for navigating Indian government services**
**Google AI Builder Cup 2026 · Working prototype**

[Live prototype](https://maadhyam-1610.web.app) · [QA evidence](qa/evidence/after-firebase-fix/execution.json) · [QA documentation](qa/README.md)

## Problem and solution

Citizens navigating government services may encounter differing document requirements, inconsistent names, dates of birth or addresses, and uncertainty about which correction to make first. **Maadhyam** combines document intelligence, explainable rule evaluation and dependency-aware planning to help citizens prepare before visiting official government channels.

> **Independent prototype:** Maadhyam is not an official government portal. It does not issue documents, submit government applications, or guarantee eligibility, acceptance or approval.

## Capabilities

| Area | Prototype capabilities |
| --- | --- |
| Document intelligence | OCR-assisted extraction, document categorization, Indian name matching and discrepancy detection |
| Rules and guidance | Service checklists, rules-as-code, explanatory findings and official guidance references |
| Correction planning | Prerequisites, dependency-aware correction paths, minimum-review recommendations and proof substitution options |
| Scenario exploration | What-if simulations, deadlines, bottlenecks and modeled cost/day/visit trade-offs |
| Citizen experience | Service discovery, guided preparation, AI assistance and document-management workflows |
| Multi-department foundation | Passport-focused guided journey and extensible Aadhaar/EPFO rule-pack foundations |

**Scope:** Passport is the primary guided prototype journey. Other catalogue entries or advanced workflows may be informational, simulated or marked *Coming Soon*. Planning outputs are not official government determinations.

## Live demo

**https://maadhyam-1610.web.app**

1. Explore the citizen service catalogue and open the Passport preparation journey.
2. Where supported, upload **fictional** documents from [`demo/fictional_documents/`](demo/fictional_documents/).
3. Review extracted information, potential discrepancies and explanatory guidance.
4. Explore available correction planning, prerequisites and what-if scenarios.
5. Review preparation tasks and the AI assistance interface, where configured.

**Privacy:** Review the sample PDFs before public release to ensure no real personal identifiers are present. Do not use real identity documents in the public demo.

## Architecture

```text
Citizen / Browser
       |
React + TypeScript / Vite
       |
       +---- Firebase authentication and configured data services
       |
Python FastAPI backend
       |
       +---- Document extraction and discrepancy analysis
       +---- Rule packs and dependency-aware planning
       +---- Gemini / Vertex AI integration (when configured)
       +---- Configured cloud document/data services
```

| Layer | Technology |
| --- | --- |
| Frontend | React, TypeScript, Vite |
| Backend | Python, FastAPI |
| AI | Google Gemini / Vertex AI integration |
| Hosting | Firebase Hosting and Google Cloud Run |
| Cloud services | Firebase Authentication and configured Google Cloud / Firebase services |
| Validation | Pytest, automated browser tests, HTTP tests, frontend lint/build and regression suites |

## Repository structure

```text
Maadhyam-prototype/
├── Maadhyam/
│   ├── apps/
│   │   ├── api/             # FastAPI backend
│   │   └── web/             # React + TypeScript frontend
│   ├── firebase.json
│   └── package.json
├── demo/
│   └── fictional_documents/
├── qa/
│   ├── run_final.py
│   ├── README.md
│   └── evidence/
│       └── after-firebase-fix/
└── README.md
```

## Local development

Prerequisites: compatible Node.js/npm, Python and [uv](https://docs.astral.sh/uv/). Cloud-backed workflows require authorized environment configuration.

**Backend** — from repository root:

```bash
cd Maadhyam/apps/api
uv sync --extra dev
uv run --extra dev python -m uvicorn maadhyam_api.main:app --app-dir src --reload --port 8000
```

API docs: `http://127.0.0.1:8000/docs`.

**Frontend** — in another terminal, from repository root:

```bash
cd Maadhyam/apps/web
npm ci
npm run dev
```

Use the URL printed by Vite. Never commit `.env`, `.env.local`, credentials or service-account keys.

## Quality assurance

**Final local validation: 18 October 2026. All 11 QA execution stages passed.**

| Validation | Verified outcome |
| --- | --- |
| Backend tests | **463 passed** |
| Browser tests | **284 passed**, one warning |
| Frontend lint | Passed |
| Frontend production build | Passed |
| Test collection | Passed |
| HTTP tests | Passed |
| Legacy functional suite | Passed |
| Legacy reasoning suite | Passed |
| Legacy M9 suite | Passed |
| Legacy vault suite | Passed |
| Legacy smoke suite | Passed |

**747 backend and browser tests passed.** Other suites are listed separately to avoid double-counting.

### Inspect the evidence

- [Consolidated execution summary](qa/evidence/after-firebase-fix/execution.json)
- [Backend log](qa/evidence/after-firebase-fix/backend.log) · [Backend JUnit XML](qa/evidence/after-firebase-fix/backend.xml)
- [Browser log](qa/evidence/after-firebase-fix/browser.log) · [Browser JUnit XML](qa/evidence/after-firebase-fix/browser.xml)
- [Frontend build log](qa/evidence/after-firebase-fix/frontend-build.log) · [Frontend lint log](qa/evidence/after-firebase-fix/frontend-lint.log)
- [QA documentation](qa/README.md)

To reproduce after installing dependencies, from repository root:

```bash
MAADHYAM_FINAL_QA_OUTPUT=qa/evidence/local-run \
  Maadhyam/apps/api/.venv/bin/python qa/run_final.py
```

Browser tests require supported browser automation dependencies and frontend test configuration. The successful run used local services with **live providers disabled** (`"liveProviders": false`); it is not a production load-test or government integration certification.

## Deployment references

- [Google Cloud deployment guide](qa/MAADHYAM_MANUAL_GOOGLE_CLOUD_DEPLOYMENT_GUIDE.md)
- [Manual cloud deployment handoff](qa/M12_1_MANUAL_CLOUD_DEPLOYMENT_HANDOFF.md)
- [Deployment and smoke-test report](qa/FINAL_DEPLOYMENT_AND_SMOKE_TEST_REPORT.md)

Review cloud permissions, billing, credentials and storage access before deployment.

## Responsible use and limitations

- Official government portals and authorities remain the source of truth.
- AI-extracted information and recommendations may be inaccurate and need human review.
- Correction routes, durations and costs may be illustrative.
- Do not upload genuine identity documents to a public demonstration.
- Maadhyam does not submit government applications or guarantee outcomes.

## Team

Swarada Jalukar · Shreyas Chaudhari · Darshana Ranalkar · Aditya Phadke

---

*Built for the Google AI Builder Cup 2026.*
