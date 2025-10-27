# BOTE Worksheet (Fill Me In)

## Assumptions
- Users: ______
- Concurrency (peak): ______
- Actions/user/day: ______
- Payload size (bytes or MB): ______
- SLOs: p95 ______ ms; Availability ______ %
- Retention: ______ days; Replication: ______×; Compression: ______×
- Regions: ______ (single / multi-region)

## Load
- Ops/day = ______________________
- Avg RPS = Ops/day / 86,400 = ______________________
- Peak RPS (×____) = ______________________

## Storage
- Bytes/event × events/day = __________ bytes/day = __________ GB/day
- After compression (×____) & replication (×____) = __________ GB/day
- Retained (× days) = __________ TB

## Bandwidth
- Concurrency × bitrate_Mbps = __________ Mbps = __________ Gbps
- Per-user MB/hour = (Mbps ÷ 8) × 3600 ÷ 1024 = __________

## Latency
- Sequential Σ = __________ ms
- Parallel max + overhead = __________ ms

## Compute
- CPU-sec/s = RPS × CPU_ms / 1000 = __________
- Cores @ ____% util = __________

## Availability
- Allowed downtime/month @ ______% = __________ minutes

## Risks & Mitigations
- Bottleneck: __________ → Mitigation: __________
- Trade-off: __________ → Rationale: __________
