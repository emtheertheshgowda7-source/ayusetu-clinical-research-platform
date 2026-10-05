# AyuSetu

AIIA Clinical Research Intelligence & Pharmacovigilance Platform — portable local demo.

## Run

No build step or external service is required.

```bash
python3 -m http.server 4173
# open http://localhost:4173
```

Use the local server so the browser can load the synthetic JSON fixture without file-origin restrictions.

## Demo access

- Email: `pi@aiia.example`
- Password: `demo`
- Role: Principal Investigator

The login is a synthetic demo gate only. Do not use real patient, institutional, or authentication data.

## Included scope

- Role-aware enterprise shell with persistent light/dark theme
- Portfolio dashboard with operational, data-quality, safety, and compliance KPIs
- Studies, sites, participants, recruitment, visits, monitoring, deviations, data quality, pharmacovigilance, compliance, reports, documents, audit trail, integrations, and administration modules
- Study detail drawer with lifecycle milestones
- Search, filters, notification panel, command palette, responsive sidebar, toasts, and CSV export
- Synthetic data and client-side state only
- Architecture, API boundary, data model, security, and phased delivery documentation

## Production path

The demo intentionally uses browser data so it can be evaluated offline. Replace `src/mock-data.js` concepts with a service layer backed by PostgreSQL, an OIDC/MFA provider, immutable audit storage, object storage, FHIR R4 endpoints, and CDISC export workers. See `docs/ARCHITECTURE.md`.

## Safety and compliance note

This is a product prototype, not a validated clinical system or regulatory authority. Safety signal and coding screens remain human-review workflows. All values are synthetic.
