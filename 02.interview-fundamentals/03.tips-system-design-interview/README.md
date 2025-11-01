# System Design Interview — Things to Avoid (and What To Do Instead)

A concise, practical README to keep you from common pitfalls during system design interviews—and show a thoughtful, adaptable approach.

---

## TL;DR Checklist

* [ ] Clarify requirements, scope, and constraints before proposing an architecture
* [ ] Start with a high‑level design, then zoom into key components
* [ ] Consider alternative designs; adapt to hints
* [ ] Explicitly discuss trade‑offs and justify choices
* [ ] Cover non‑functional requirements (NFRs) and real‑world constraints
* [ ] Communicate clearly, engage the interviewer, and think aloud
* [ ] Acknowledge unknowns; make reasonable assumptions
* [ ] Summarize decisions and risks at the end

---

## The Don’ts → Do This Instead

### 1) Don’t Ignore the Requirements

**Avoid:**

* Skipping clarification questions
* Oversimplifying the problem and missing edge cases

**Do instead:**

* Ask: *Who are the users? What’s in/out of scope? Target scale & SLAs?*
* Capture constraints (read/write mix, geo regions, latency budgets, privacy/compliance).

### 2) Don’t Dive into Details Too Soon

**Avoid:**

* Starting with DB schemas, APIs, or specific technologies immediately
* Losing the big‑picture architecture

**Do instead:**

* Draw a high‑level block diagram first (clients → gateways → services → data → infra)
* Identify 2–3 bottlenecks to deep‑dive later (e.g., feed ranking, hot keys, cache strategy)

### 3) Don’t Stick Rigidly to One Idea

**Avoid:**

* Defending the first design to the death
* Ignoring interviewer hints

**Do instead:**

* Compare at least two approaches (e.g., **fan‑out on write** vs **fan‑out on read**)
* Say: *“If traffic is X, I’d switch to Y because…”*

### 4) Don’t Overlook Trade‑offs

**Avoid:**

* Presenting choices without pros/cons
* Making claims without rationale

**Do instead:**

* State explicit trade‑offs: availability vs consistency, latency vs cost, simplicity vs flexibility
* Justify defaults (e.g., **read‑heavy** → caches & replicas; **write‑heavy** → queues & batching)

### 5) Don’t Neglect Non‑Functional Requirements

**Avoid:**

* Focusing only on features
* Ignoring cost, operability, or platform constraints

**Do instead:**

* Cover NFRs: scalability, availability, consistency, latency, durability, cost, security, compliance, observability, operability
* Note constraints: team expertise, cloud/vendor limits, time‑to‑market

### 6) Don’t Under‑Communicate

**Avoid:**

* Silent sketching or disorganized explanations
* Monologuing without checkpoints

**Do instead:**

* Narrate decisions, invite feedback: *“I’ll propose A, then validate capacity, then discuss failure modes.”*
* Use structure and signposting; recap after each section

### 7) Don’t Be Overconfident or Arrogant

**Avoid:**

* Dismissing feedback or unknowns
* Over‑promising

**Do instead:**

* Admit uncertainty, propose experiments or phased rollouts
* Frame assumptions and risks explicitly

---

## Interview Flow Template (30–45 mins)

1. **Clarify & Scope (3–5m):** Users, use cases, scale, SLAs, constraints
2. **High‑Level Design (5–8m):** Core components, data flow, request lifecycle
3. **Data & Storage (5–7m):** Access patterns, schema model, partitioning, indexing
4. **Performance & Scale (6–8m):** Caching, queues, replication, sharding, backpressure
5. **Reliability & Ops (5–7m):** Failover, retries, idempotency, rate limits, monitoring, alarms
6. **Trade‑offs & Alternatives (3–5m):** Why this approach vs another; when to pivot
7. **Wrap‑up (2–3m):** Summary, risks, next steps, MVP vs future phases

> **Time‑box:** If the interviewer dives deep, narrate the re‑prioritization: *“I’ll pause the cache section and focus on consistency modes next.”*

---

## Quick Trade‑off Axes (Mention Explicitly)

* **Availability vs Consistency:** AP vs CP (per CAP) under network partitions; read‑after‑write vs eventual
* **Latency vs Throughput:** Hot path optimization vs batch/async processing
* **Cost vs Performance:** Vertical scaling vs horizontal; reserved vs on‑demand
* **Simplicity vs Flexibility:** Managed services vs bespoke infra
* **Freshness vs Efficiency:** Cache TTL, write‑through vs write‑back

---

## Non‑Functional Requirements (NFR) Prompt

Use this mnemonic to check coverage: **SCALE DOCS**

* **S**calability, **C**onsistency, **A**vailability, **L**atency, **E**lasticity
* **D**urability, **O**bservability, **C**ost, **S**ecurity/compliance

---

## Communication Scripts

* **Clarify:** “Before designing, I’ll clarify users, APIs, traffic, and SLAs.”
* **Assume:** “Given no numbers, I’ll assume 50k RPS peak, 90/10 read/write.”
* **Checkpoint:** “I’ll outline the request path, then discuss data model and scale.”
* **Trade‑off:** “I choose eventual consistency here to cut tail latency and cost.”
* **Wrap‑up:** “MVP ships with A/B/C; Phase‑2 adds geo‑replication and reindexing.”

---

## Failure Modes & Reliability Prompts

* Hot partitions / uneven keys → consistent hashing, random suffixes, per‑tenant sharding
* Thundering herds → request coalescing, token buckets, circuit breakers
* Data loss → multi‑AZ, backups, WAL, DLQs; test restores
* Idempotency → request IDs, upserts, de‑duplication windows
* Backpressure → bounded queues, shed load, degrade gracefully

---

## Capacity & Estimation (back‑of‑the‑envelope)

* RPS, payload sizes, storage growth/day, hot set size, cache hit ratio
* Read/write QPS per shard/replica; p95/p99 targets
* Cost guardrails (compute, storage, egress, managed services)

---

## Interviewer Engagement Prompts

* “Which path would you like me to deep‑dive next: cache strategy or data partitioning?”
* “If consistency requirements tighten, I’d switch from async to quorum writes.”

---

## One‑Page Printable

Keep this one‑pager in view during mock interviews:

* Clarify → High‑level → Data → Scale → Reliability → Trade‑offs → Wrap‑up
* Mention **SCALE DOCS**
* State 2 alternatives and why
* Quantify at least 3 back‑of‑the‑envelope numbers
* End with risks and phased plan

---
