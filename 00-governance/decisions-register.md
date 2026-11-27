# Decision register (D1-D16)

Source of truth for programme decisions. Mirrors plan v3.12, section 9. D17 rests on the matched-scenario like-for-like table (section 8): LOW $1.31M vs $1.47M, MID about $2.48M vs $2.84M, HIGH $3.65M vs $4.21M, buffered with the reserve outside the buffer and a $120k-$300k 24/7 placeholder on the external side; in-house about 11-13% cheaper with the reserve. Tripwire: owner hours above 30% of estimated (derivation shown in row 13; weighted slice 60%; estimates frozen in writing); soft read at end of design, firing checkpoint Aug 31, 2027 moving with the slip rule; owner pulls it. If it fires: owners finish R1 and carry the pilot; the pre-qualified vendor takes the R1b build (Feb 2028) and onboards during the pilot; reserve $100k-$350k funds vendor onboarding and codebase handover, or short-term Frappe partner help to finish R1 if the slice evidence says the owners cannot; D17 re-decided for R1b onward; worst case $1.57M-$4.45M labeled a conservative ceiling that counts R1 twice (counts R1 twice; the real firing path costs less); the 25% deduction is kept deliberately as headroom so the 30% line is slightly stricter than its derivation. Hiring evidence: market check or shortlist for the two owner roles due before Dec 8. Schedule: R3 gate signed month 31 (Aug 2029) as its own row; v17 upgrade from March 2030, after the R3 rollout and payroll cutover, with a Frappe partner support arrangement bridging v16 from its planned end of support (late 2029); the months 31-32 between-gates window stays only as the written exception if v17 is proven stable well before the R3 gate. Status as of November 27, 2026.

| ID | Decision | Owner | Deadline | Status |
|----|----------|-------|----------|--------|
| D1 | Approval matrix and spending limits | general manager, finance | Mar 31, 2027 | Open |
| D2 | Rig-site connectivity check | IT, rig managers | Jan 15, 2027 | Open |
| D3 | Historical data check | maintenance, stores, finance | Jan 31, 2027 | Checklist sent |
| D4 | AI hosting | general manager, IT, legal | Jan 2028, at the gate | Deferred on purpose |
| D5 | Where ERPNext runs | general manager, IT, legal | Mar 31, 2027 | Open |
| D6 | 12-rig status baseline | operations, contracts | Jan 15, 2027 | Template sent |
| D7 | Pilot rig | operations manager | Mar 31, 2027 | Open |
| D8 | Offline capture method | tech lead, operations | Mar 31, 2027 | Open |
| D9 | Delivery team and product owner | general manager | Dec 15, 2026 | Open (date pulled forward) |
| D10 | Acceptance thresholds | steering group | Mar 31, 2027 | Proposed |
| D11 | Throwaway prototypes during design | platform owner | - | Approved Nov 27, with guardrails |
| D12 | Offline conflict policy | tech lead, operations | Mar 31, 2027 (proposed) | Open |
| D13 | Tablet fleet management | IT, security | Mar 31, 2027 | Open |
| D14 | Copilot launch timing | general manager, IT | R1b gate (Nov 2028); D4 settles the launch month | Open |
| D15 | Official accounting books | finance, general manager | during design, before R1b build | Open |
| D16 | Drilling data rights | contracts, legal | before R3 build | Open |
| D17 | In-house or external build | general manager | Dec 8, 2026 (proposed, owner to confirm) | Open (twelfth-review numbers, Nov 27) |

Full decision text: plan v3.4, section 9.
