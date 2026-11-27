# Prototypes (decision D11)

Throwaway prototypes only, under the D11 guardrails approved November 27, 2026:

1. Live in this folder (or a separate spikes repo), never on production servers.
2. No real crew or client data, ever. Synthetic data only.
3. Each prototype is time-boxed to two or three weeks and ends with a one-page findings memo feeding decisions D8 and D12.
4. Prototypes test the hard parts: the seven-day offline queue on an actual rugged tablet, sync over a simulated poor satellite link, the PIN-and-hash signature, Arabic right-to-left rendering.
5. No prototype is ever promoted to production. Every real feature is rebuilt from the approved design.

## Candidate prototype list (from the design phase)

| ID | Subject | Feeds | Status |
|----|---------|-------|--------|
| P1 | Seven-day offline queue on a rugged tablet | D8 | Planned |
| P2 | Sync over a simulated poor satellite link | D8, D12 | Planned |
| P3 | PIN-and-hash daily-report signature | acceptance design | Planned |
| P4 | Arabic RTL daily-report form | D8 | Planned |
| P5 | Scoped, short-lived copilot session tokens (custom build; Frappe's built-in tokens are long-lived per-user keys) | DD-11 | Planned (sixth review, Nov 27) |
| P6 | Read-replica routing coverage: replica routing is opt-in per endpoint, so mark every copilot and report endpoint explicitly, add a CI test that fails when one is not replica-routed, and check how replica lag affects a just-revoked permission | DD-05 | Planned (eighth review, Nov 27) |
| P7 | Frappe-to-Superset OAuth sign-on, including server-side session store (Superset's default Flask cookie sessions cannot be revoked server-side - official security docs) and revocation on deprovisioning | DD-05 | Planned (eighth review, Nov 27) |
