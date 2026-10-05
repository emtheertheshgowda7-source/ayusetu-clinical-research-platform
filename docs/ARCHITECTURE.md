# AyuSetu production architecture

## Product boundary

AyuSetu is the system of record for study operations, oversight workflows, safety case routing, compliance evidence, and auditable portfolio intelligence. It is not a regulator and does not automatically declare a safety signal as causality or product risk.

## Reference architecture

- **Web client:** React/TypeScript enterprise shell, accessible tables/forms, route-level permission guards, offline-safe demo fixture mode.
- **API:** REST/JSON or GraphQL gateway with OIDC/MFA session validation, tenant/institution scope, idempotency keys, optimistic concurrency, and structured error envelopes.
- **Domain services:** Study, site, participant, recruitment, visit, monitoring, deviation, data quality, IEC/CTRI compliance, pharmacovigilance, reporting, documents, integrations, and administration.
- **Data:** PostgreSQL for transactional records; row-level scope controls; object storage for versioned documents; append-only audit stream with hash chaining and retention policy.
- **Workers:** Queue-backed exports, notifications, FHIR synchronization, validation, document processing, and safety aggregate calculations.
- **Interoperability:** HL7 FHIR R4 mappings for Patient (pseudonymous), ResearchStudy, ResearchSubject, Encounter, Observation, AdverseEvent, and DocumentReference. CDISC CDASH/SDTM/ADaM and Define-XML export workers.

## Core entities

`User`, `Role`, `Permission`, `Study`, `ProtocolVersion`, `Site`, `Participant`, `Consent`, `Visit`, `MonitoringVisit`, `ProtocolDeviation`, `DataQuery`, `SafetyCase`, `SafetyCoding`, `SafetySignal`, `ComplianceRequirement`, `RegulatoryMilestone`, `Document`, `AuditEvent`, `Notification`, `IntegrationJob`, `KpiSnapshot`.

## Control requirements

- Enforce least privilege and study/site scope on every read/write.
- Pseudonymize participant identifiers in dashboards; keep direct identifiers outside analytics views.
- Require human reviewer approval for medical coding and safety signal disposition.
- Capture immutable, time-stamped audit events for create/edit/approve/sign/export/permission changes.
- Encrypt in transit and at rest; keep keys in a managed KMS; never place credentials in source or fixtures.
- Preserve ALCOA+ attributes: attributable, legible, contemporaneous, original, accurate, complete, consistent, enduring, and available.
- Validate required fields, allowed visit windows, date sequences, study/site relationships, duplicate participants, and mandatory consent.

## Suggested API surface

`POST /auth/mfa/verify` · `GET /portfolio/kpis` · `GET /studies` · `POST /studies` · `GET /studies/:id` · `GET /studies/:id/timeline` · `GET /sites` · `GET /participants` · `GET /data-queries` · `POST /safety-cases` · `POST /safety-cases/:id/review` · `GET /compliance/actions` · `POST /exports/cdisc` · `POST /integrations/fhir/jobs` · `GET /audit-events`.

## Delivery phases

1. Core CTMS, RBAC, audit, KPI, IEC/CTRI, recruitment, monitoring, deviations, data quality.
2. AE/ADR/SAE workflow, coding dictionaries, safety review, signal review, DSMB reporting.
3. FHIR R4/ABDM integration adapters and external EDC/HIS synchronization.
4. CDISC exports with Define-XML and validation reports.
5. Advanced analytics with explainable signals, cohort comparisons, and human approval gates.
6. Security, performance, backup/restore, accessibility, validation, and operational readiness.
