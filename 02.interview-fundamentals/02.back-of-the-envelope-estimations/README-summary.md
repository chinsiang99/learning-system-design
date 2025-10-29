# Back-of-the-Envelope Estimation (5-Minute Playbook)

A fast workflow to size a system in interviews. In ~5 minutes, cover **traffic**, **storage**, **bandwidth**, and **memory** (cache). Traffic + storage is often sufficient, but adding bandwidth & memory shows depth.

---

## 0) Inputs to Ask the Interviewer
- **DAU / concurrency** (peak factor if known)
- **Reads/day & writes/day** (or typical user actions/day)
- **Payload sizes** (text/photo/video, average + range)
- **Retention** (how long to keep data), **replication/compression**
- **Latency & availability targets** (p95/p99, SLA/SLO)
- **Read:Write ratio** (e.g., 50:1 for most consumer apps; write-heavy for logs/metrics)

---

## 1) Traffic (RPS)
**Goal:** convert daily counts → per-second.

- `avg_rps = ops_per_day / 86,400`
- `peak_rps ≈ avg_rps × (2–5×)` when in doubt.

**Example (from notes):**  
- Writes/day = **1,000,000** ⇒ `1,000,000 / 86,400 ≈ 11.6 RPS`  
  *Napkin:* round to **~10 RPS** for speed.  
- Read:Write = **50:1** ⇒ Reads/day = **50,000,000** ⇒ `≈ 579 RPS`  
  *Napkin:* **~500 RPS**.

**Takeaways:** System is **read-heavy**; plan for read scaling (cache, replicas, CDN).

---

## 2) Storage
**Goal:** size per-item × volume × retention × factors.

- `daily_bytes = events_per_day × bytes_per_event`
- Apply **compression** (e.g., 0.5×) then **replication** (e.g., 3×).
- `retained_storage = daily_storage × retention_days`

**Item size (pastebin):**  
200 lines × 10 words/line × 5 chars/word × **1 B/char** = **10,000 B ≈ 10 KB**.

**Daily writes:**  
1,000,000 pastes/day × **10 KB** ≈ **10 GB/day** (SI).  
(= 10,000,000,000 B ≈ **9.31 GiB/day** in IEC)

**Retention (5 years):**  
10 GB/day × 365 × 5 = **18.25 TB** → *Napkin round-up:* **~20 TB**.  
With **3× replication**: **~55 TB** exact, **~60 TB** napkin.

---

## 3) Bandwidth
**Goal:** bytes per second in/out.

- **Inbound (writes):** `write_rps × item_size`
- **Outbound (reads):** `read_rps × item_size`
- **Convert:** `MB/s = Mbps ÷ 8`

**Example:**  
- Inbound: 10 KB × **~10–12 RPS** ≈ **0.10–0.12 MB/s** (≈ **100–116 KB/s**)  
- Outbound: 10 KB × **~500–580 RPS** ≈ **5.0–5.8 MB/s**  
(*Bandwidth headroom:* design for peaks + overhead.)

---

## 4) Memory (Caching)
**Goal:** estimate cache size for hot content.

- **80/20 heuristic:** ~20% of items drive ~80% of reads.
- **Upper bound (naive):** `reads_per_day × item_size × hot_fraction`  
  From notes: 50M reads/day × 10 KB × 0.2 → **~100 GB/day of read bytes** (this is **traffic**, not unique set).
- **Better cache sizing:** estimate **unique hot set** over **cache TTL**.
  - If **1M new items/day**, **20% hot** over a **1-day TTL** ⇒ **200k items × 10 KB ≈ 2 GB** cache.
  - Real cache need is **≤ 2 GB** after de-dup and compression.

**Takeaway:** Quote both: **upper-bound traffic view** (~100 GB/day) and **unique-hot-set view** (~2 GB).

---

## 5) App Server Sizing (very high level)
**Decide bound:** CPU vs I/O vs memory. For **CPU-bound**:

- `server_rps ≈ cores × (1 / cpu_sec_per_req) × target_util`
  - Example: 8 cores, **0.5 s CPU/req**, 70% util ⇒ `8 × 2 × 0.7 = 11.2 RPS/server`
- **Servers needed:** `total_rps / server_rps`
  - With **~500 RPS** reads ⇒ `500 / 11.2 ≈ 45` servers  
  - *Without util* (your note’s 8/0.5=16 RPS): `500 / 16 ≈ 31` servers  
**Plan for HA & bursts:** quote **~30–60** nodes depending on assumptions.

---

## Quick Conversions (put these on the whiteboard)
**Bits/Bytes:** 1 B = 8 b  
**SI (decimal):** 1 KB=1,000 B; 1 MB=1,000,000 B; 1 GB=1e9 B; 1 TB=1e12 B  
**IEC (binary):** 1 KiB=1,024 B; 1 MiB=1,048,576 B; 1 GiB=1,073,741,824 B  
**Bridges:** 1 MB ≈ 0.9537 MiB; 1 GB ≈ 0.9313 GiB  
**Time:** 1 day=86,400 s; 1 h=3,600 s; 1 s=1,000 ms  
**Bandwidth:** MB/s = Mbps ÷ 8; GB/h ≈ (Mbps ÷ 8) × 3600 ÷ 1024

---

## Handy “Numbers Everyone Should Know” (sanity checks)
- L1 ref ~0.5 ns • RAM ~100 ns • same-DC RTT ~0.5 ms  
- Disk seek ~10 ms • Read 1 MB from disk ~30 ms • Over network ~10 ms  
- Inter-continent RTT ~150 ms  
*Use as bounds, not SLAs.*

---

## Common Sizes (Language & Media)
**Language**
- ~10 words/line, ~5 chars/word → **~50 chars/line ≈ 50 B** (ASCII)
- “English words” (dictionary) **~500k** (order-of-magnitude for index sizing)

**Media (rules of thumb)**
- **HD image (1280×720)** raw: 1280×720×3 B ≈ **2.76 MB**; JPEG often **100–500 KB**; napkin **~3 MB** upper bound
- **Profile image (300×300)** raw ≈ **0.27 MB**; compressed **~30–300 KB** (napkin **~300 KB**)
- **HD video 1 minute** ≈ **~50 MB** (e.g., per-frame 3 MB × 30 fps × 1/100 compression × 60 s ≈ 54 MB)
- **Multi-resolution ladder (1080p + 720/480/360/240/144p):** store ≈ **~2×** the 1080p size → **~100 MB/min** budget

---

## 5-Minute Checklist (what you say out loud)
1. **Scope & assumptions**: DAU, reads/writes/day, item size, retention, targets.
2. **Traffic**: compute **avg & peak RPS**, call out read-heavy ratio (e.g., 50:1).
3. **Storage**: item size → **GB/day**, then **TB/retention** → apply **compression/replication**.
4. **Bandwidth**: inbound/outbound **MB/s** (peak), note CDN/caching impact.
5. **Memory**: cache **unique hot set** (80/20, TTL) → **GB**.
6. **Server count** (optional): CPU-bound formula; quote a **range** with headroom.
7. **Risks & mitigations**: hot keys, tail latency, invalidation, backpressure.

---

## Worked Summary (Pastebin-like Example)
- **Writes/day:** 1,000,000 → **~11.6 RPS** (≈ **10** napkin)
- **Reads/day:** 50,000,000 → **~579 RPS** (≈ **500** napkin)
- **Item size:** **~10 KB**
- **Storage/day:** **~10 GB** → **~18.25 TB over 5y** (round **~20 TB**); **×3 repl ≈ ~55–60 TB**
- **Bandwidth:** **in ~0.1–0.12 MB/s**, **out ~5.0–5.8 MB/s** (avg; design for peaks)
- **Cache (1-day TTL):** upper-bound traffic view **~100 GB/day of read bytes**; **unique hot-set ~2 GB**
- **Servers (CPU-bound):** **~31–45 nodes** depending on utilization assumption; quote **~30–60** for HA

---

## Pitfalls
- Mixing **bits vs bytes** or **SI vs IEC**
- Designing to **averages**; ignore **peaks/tails**
- Counting **reads** instead of **unique hot items** for cache sizing
- Applying **replication** before **compression** in storage math
- Assuming **linear scale** without coordination/lock/IO overhead

