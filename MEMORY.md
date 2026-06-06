# MEMORY.md

Session memory for cross-session continuity. Updated by Claude Code at decision checkpoints.

---

## Session Handoff

### 2026-06-06 — HIVE-115 Phase C ADR-011 decision checkpoint

**Decision: HOLD on PR-4 (Outbox + detect-and-defer, ADR-009 v2 + ADR-010)**

**Signals checked (14 days post-v1.18.0 / bounded_call ship 2026-05-23):**
- Issue #110 (`vault tool latency tail`): **CLOSED** (completed 2026-05-23) — the zombie-subprocess / git-lock-contention driver for PR-4 is resolved.
- New latency / ghost_response issues filed: **zero**. Only open issues are #212 (test isolation debt), #201 (agent identity vault SSOT), #176 (Phase C daemon activation), #127 (compat shim deadline).
- CI health: **all green** post-v1.18.0.
- Open PRs: **none**. `feat/HIVE-115-pr4-outbox-defer` branch does not exist on remote.

**Conclusion:** bounded_call alone is sufficient for current workloads. No recurrence of the failure mode documented in #110. PR-4 complexity is not warranted.

**Next mandatory actions (in priority order):**
1. **#127 due 2026-06-12** — Evaluate upstream `modelcontextprotocol/python-sdk#2610`. If still silent, port `_compat.py` fix as upstream PR. Six days from today.
2. **#176** — Phase C daemon activation / rollout (`hive client` + per-OS service units). Exit criterion for HIVE-118.
3. **PR-4 re-evaluate** — Reopen if any ghost_response or obsidian-git lock contention surfaces post-v1.18.0. Criteria: any new latency issue OR #110 re-opened.
