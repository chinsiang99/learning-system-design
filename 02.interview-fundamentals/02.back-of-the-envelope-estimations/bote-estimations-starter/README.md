# Back-of-the-Envelope (BOTE) Estimations — System Design Interview Kit

Fast, defensible napkin math to size systems, spot bottlenecks, and justify trade-offs. This repo gives you:
- A **conversions cheat sheet** (SI vs IEC, time, bandwidth, availability → downtime, etc.)
- A **worksheet** to structure your estimates in interviews
- A **notebook** with ready-made functions for common calculations
- **Issue & PR templates** so you can track improvements like a real project

## Quickstart
1. Skim **CONVERSIONS.md** for the unit system and formulas.
2. Open **worksheets/BOTE_Worksheet.md** and fill in assumptions.
3. (Optional) Run **notebooks/Sample_Estimations.ipynb** to compute RPS, storage, bandwidth, cores, and downtime.
4. In your interview, state assumptions, compute, sanity-check, and call out trade-offs tied to SLOs.

## Repo Structure
```
.
├── README.md
├── CONVERSIONS.md
├── worksheets/
│   └── BOTE_Worksheet.md
├── notebooks/
│   └── Sample_Estimations.ipynb
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── bug_report.md
    │   └── feature_request.md
    └── pull_request_template.md
```

## Included Examples
- Social feed post load → **RPS** and peak factor
- Photo storage per day → **PB/day** with replication & compression
- Streaming bandwidth → **Gbps/Tbps** aggregate egress
- Fan-out API latency → **sequential vs parallel**
- CPU sizing → **cores at target utilization**
- Availability target → **allowed downtime per month**

## License
MIT. Use at your own risk; numbers are heuristics for estimation, not SLAs.
