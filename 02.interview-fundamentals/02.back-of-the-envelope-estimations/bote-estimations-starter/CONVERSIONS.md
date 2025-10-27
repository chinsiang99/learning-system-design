# CONVERSIONS.md — Units, Formulas, and Handy Numbers

> **Rule #1:** Always label **bits vs bytes**, **SI vs IEC**, and time windows (per second, per hour, per day).

---

## 1) Data Units (Bytes) — SI vs IEC
**SI (decimal):** 1 KB = 1,000 bytes; 1 MB = 1,000,000 bytes; 1 GB = 1,000,000,000 bytes  
**IEC (binary):** 1 KiB = 1,024 bytes; 1 MiB = 1,024 KiB = 1,048,576 bytes; 1 GiB = 1,024 MiB

| Unit | SI (×10³) | IEC (×2¹⁰) | Approx Relation |
|---|---:|---:|---|
| KB / KiB | 1,000 | 1,024 | 1 KB ≈ 0.9766 KiB |
| MB / MiB | 1,000,000 | 1,048,576 | 1 MB ≈ 0.9537 MiB |
| GB / GiB | 1,000,000,000 | 1,073,741,824 | 1 GB ≈ 0.9313 GiB |
| TB / TiB | 10¹² | 1,099,511,627,776 | 1 TB ≈ 0.9095 TiB |
| PB / PiB | 10¹⁵ | 1,125,899,906,842,624 | 1 PB ≈ 0.8882 PiB |

**Conversions**
- Bytes ↔ bits: **1 byte = 8 bits**; **Bps = bps ÷ 8**
- SI → IEC: `MiB = MB × 1,000,000 / 1,048,576 ≈ MB × 0.9537`
- IEC → SI: `MB = MiB × 1,048,576 / 1,000,000 ≈ MiB × 1.048576`

---

## 2) Network Throughput (bits per second)
| Name | Symbol | Factor |
|---|---|---:|
| bit per second | bps | 1 |
| kilobit/s | Kbps | 10³ |
| megabit/s | Mbps | 10⁶ |
| gigabit/s | Gbps | 10⁹ |
| terabit/s | Tbps | 10¹² |

**Common conversions**
- **MB/s = Mbps ÷ 8**; **GB/s = Gbps ÷ 8**
- **Data moved over time:** `GB/hour = (Mbps ÷ 8) × 3600 ÷ 1024`

**Example:** 4 Mbps stream → `4/8 = 0.5 MB/s` → `0.5 × 3600 ≈ 1800 MB/h ≈ 1.76 GB/h`

---

## 3) Time Units
- 1 s = **1000 ms** = **1,000,000 μs** = **1,000,000,000 ns**
- 1 min = **60 s**
- 1 hour = **3600 s**
- 1 day = **86,400 s**
- **RPS from daily ops:** `RPS = ops_per_day / 86,400`

---

## 4) Availability → Allowed Downtime
| Availability | Max Downtime / Month (30 days) | / Week | / Day |
|---:|---:|---:|---:|
| 99.0% | 7 h 12 m | 1 h 41 m | 14 m 24 s |
| 99.5% | 3 h 36 m | 50 m 24 s | 7 m 12 s |
| 99.9% | 43 m 12 s | 10 m 5 s | 1 m 26 s |
| 99.95% | 21 m 36 s | 5 m 2 s | 43 s |
| 99.99% | 4 m 19 s | 1 m 0 s | 8.6 s |
| 99.999% | 26 s | 6 s | 0.86 s |

**Formulas**
- `allowed_downtime = (1 - availability) × window_duration`
- `window_duration` in seconds/minutes for day/week/month/quarter/year

---

## 5) Latency Building Blocks (“Numbers Everyone Should Know”)
Operation | Time
---|---
L1 cache reference | **0.5 ns**
Branch mispredict | **5 ns**
L2 cache reference | **7 ns**
Mutex lock/unlock | **100 ns**
Main memory reference | **100 ns**
Compress 1 KB (Zippy) | **10 μs**
Send 2 KB @ 1 Gbps | **20 μs**
Read 1 MB sequentially from memory | **250 μs**
Same-DC RTT | **500 μs**
Disk seek | **10 ms**
Read 1 MB sequentially from network | **10 ms**
Read 1 MB sequentially from disk | **30 ms**
Intercontinental RTT (CA↔NL↔CA) | **150 ms**

> Use these as sanity checks, not SLAs.

---

## 6) Core Estimation Formulas

### Load (RPS/QPS)
- `avg_rps = events_per_day / 86,400`
- `peak_rps ≈ avg_rps × (2–5×)` (choose a factor)

### Storage
- `daily_bytes = events_per_day × bytes_per_event`
- After **compression** and **replication**: `effective = daily_bytes × compression_factor × replication_factor`  
  (e.g., compression 0.5, replication 3.0 → ×1.5)

### Bandwidth
- `aggregate_Mbps = concurrent_users × bitrate_Mbps`
- `egress_Gbps = aggregate_Mbps / 1000`
- `MB/s = Mbps ÷ 8`

### Latency (sequential vs parallel)
- Sequential: `Σ component_latencies`
- Parallel fan-out: `max(component_latencies) + overhead`

### Compute (CPU cores)
- `cpu_sec_per_sec = RPS × cpu_ms_per_req / 1000`
- `cores_needed = cpu_sec_per_sec / target_util` (e.g., 0.6–0.7)

### Concurrency (Little’s Law)
- `in_flight = arrival_rate/s × average_latency/s`

---

## 7) Speed of Light (baseline RTT)
- **In fiber:** ≈ **200,000 km/s** → **~5 μs per km**
- **Propagation RTT estimate:** `RTT_min ≥ 2 × distance_km × 5 μs` (not counting switching/queuing)

---

## 8) Common Pitfalls
- Mixing **bits** and **bytes**
- Forgetting **peak** vs **average**
- Applying **replication** before **compression** (order matters in storage accounting)
- Ignoring **tail latencies** (p99 >> p50)
- Assuming **linear scaling** without contention/overhead
