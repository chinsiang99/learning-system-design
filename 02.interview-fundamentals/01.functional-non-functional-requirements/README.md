# Functional vs Non-Functional Requirements (System Design Interviews)

A crisp guide to identify, balance, and communicate **what** a system must do and **how** it must behave.

---

## TL;DR
- **Functional (FR):** The *features* — user flows and system capabilities.
- **Non-Functional (NFR):** The *qualities* — performance, scale, reliability, security, cost, etc.
- Great answers state FRs, quantify NFRs, call out trade-offs, and justify architecture with SLOs.

---

## 1) Definitions

**Functional Requirements (FR) — “What”**
Describe system behaviors and use cases.
- Examples: Authenticate users; browse products → add to cart → checkout; generate reports.

**Non-Functional Requirements (NFR) — “How”**
Quality attributes and constraints shaping the architecture.
- Examples: Scalability, Performance, Availability, Security, Reliability, Observability, Maintainability, Cost.

---

## 2) Why They Matter in Interviews
- **FRs** prove you can deliver core value.
- **NFRs** prove your system is realistic, resilient, and production-grade.
- Interviewers assess your ability to **probe, quantify, and trade off** constraints.

---

## 3) Quick Examples

**FRs**
- Validate credentials; issue tokens with role-based access.
- Product catalog browsing; cart; payment; order tracking.
- Scheduled report generation with export & email.

**NFRs (make them measurable)**
- **Performance:** p95 read < 150 ms, p95 write < 300 ms.
- **Throughput:** ≥ 5k RPS steady; 3× burst for 10 minutes.
- **Availability:** 99.95% monthly; single-region failure tolerant.
- **Security:** OAuth2/OIDC; encrypt data in transit/at rest; least-privilege IAM.
- **Scalability:** Horizontal scale to 10× traffic in 1 hour.
- **Reliability/Durability:** No data loss; RPO ≤ 1 min, RTO ≤ 15 min.
- **Observability:** 3 golden signals (latency, traffic, errors) with alerts.

---

## 4) Interview Flow (Use This Template)

1. **Clarify scope & users**
   - Who, what core use cases, success criteria.
2. **List FRs**
   - Top 3–5 flows; acceptance criteria per flow.
3. **Quantify NFRs**
   - Traffic model, latency targets, SLOs, data size, growth.
4. **High-level design**
   - API surface, storage choices, caching, async vs sync, consistency model.
5. **Trade-offs**
   - Read vs write optimization, consistency vs availability, cost vs latency.
6. **Deep dive**
   - Hot path + failure modes + back-pressure + retries + idempotency.
7. **Wrap-up**
   - How design meets SLOs; phased rollout; observability & on-call.

---

## 5) One-Page Requirement Matrix (Example)

| Type | Requirement | Acceptance Criteria |
|---|---|---|
| FR | User login | Valid creds → JWT (15 min TTL); 2FA optional |
| FR | Checkout | Payment auth ≤ 3 s; idempotent per `idempotency-key` |
| NFR | Latency | p95 GET /product ≤ 150 ms; p95 POST /order ≤ 300 ms |
| NFR | Availability | 99.95% monthly; zero single-AZ SPOF |
| NFR | Scalability | 5k RPS base, 15k RPS burst; autoscale < 5 min |
| NFR | Security | TLS 1.2+; AES-256 at rest; least-privilege IAM |
| NFR | Reliability | RPO ≤ 1 min (streaming CDC); RTO ≤ 15 min |
| NFR | Observability | Traces for top 5 endpoints; SLO burn alerts |

---

## 6) Prioritization & Trade-offs
- **Prioritize:** MoSCoW or Impact/Effort. Lock SLOs early.
- **Trade-offs examples:**
  - **Cache to hit latency SLO** → stale reads risk; add TTL & cache invalidation.
  - **Strong consistency** → higher write latency; consider CQRS or bounded staleness.
  - **Multi-region active-active** → latency gains vs complexity & cost.

---

## 7) Red Flags (Avoid Vague NFRs)
- “Fast” → say **p95 150 ms**.
- “Highly available” → say **99.95%**, failover plan, chaos testing.
- “Secure” → name **standards, controls, and audits**.

---

## 8) Ready-to-Use Prompts (During Interviews)
- “What are the peak TPS and growth rates?”
- “Which user path is most latency-sensitive?”
- “What’s acceptable staleness and consistency level?”
- “RPO/RTO (Recovery Point Objective / Recovery Time Objective) targets and multi-region expectations?”
- Note that Recovery point objective here means maximum amount of data loss a business can tolerate
- Note that Recovery time objective here means aximum acceptable downtime after an outage

---

## 9) Deliverables Checklist
- [ ] FR list with acceptance criteria
- [ ] Quantified NFRs (SLOs/SLA targets)
- [ ] Capacity & traffic model (QPS, payloads, data growth)
- [ ] Architecture diagram + data flow
- [ ] Failure modes, retries, idempotency
- [ ] Observability plan (metrics, logs, traces, alerts)
- [ ] Rollout plan (canary, feature flags), cost guardrails

---

## Appendix: Glossary
- **SLA/SLO/SLA:** Availability & performance targets (external vs internal).
- **RPO/RTO:** Max data loss / recovery time after incidents.
- **CQRS:** Separate read/write paths to optimize scale & latency.
- Command Query Responsibility Segregation, is a software design pattern that separates a system's read and write operations into distinct models

