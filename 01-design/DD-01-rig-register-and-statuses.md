# DD-01: Rig register and fleet statuses

Status: DRAFT v0.1 (Nov 27, 2026) - for owner review. Nothing here is built; production code waits for the owner's design approval.
Release: R1. Feeds decisions: D6 (12-rig status baseline). Every other design document keys off Rig_ID.

## 1. Purpose

One register holds every rig the company owns or operates, current and historical. A rig is a record, not a copy of the software: adding rig 13 is settings, not code. The register is the anchor for contracts, daily reports, billing, permissions and every later module.

## 2. Rig_ID: permanent keys

- Format: `RIG-NN` (RIG-01 to RIG-12 today), assigned once, never reused, never renumbered - even if a rig is sold, scrapped or renamed. A retired rig keeps its ID with status `Retired`.
- The rig's everyday name is a field, not the key. Names change (rebranding, client contracts); the key does not.
- Every record anywhere in the system that touches a rig stores Rig_ID. Reports may show the name; the database stores the key.

## 3. Register fields (proposed)

Identity:
| Field | Type | Notes |
|-------|------|-------|
| rig_id | text, key | RIG-NN, immutable |
| rig_name | text | current working name |
| rig_type | select | drillship / jack-up / land rig / workover - PROPOSED list, confirm from records |
| rated_capacity | text | e.g. hookload or depth rating, as recorded today |
| mast_derrick_category | select | API RP 4G category, drives R1b inspection categories |
| year_built | number | |
| ownership | select | owned / leased / managed |

Current state:
| Field | Type | Notes |
|-------|------|-------|
| current_status | select | see section 4 |
| status_since | date | derived from the latest status event |
| current_contract | link -> Contract | R1 contract register; empty when uncontracted |
| current_location | text | field or area name, free text for now |
| client | link -> Client | from the current contract, not typed by hand |

Everything above is a proposal until checked against the owner's Excel records (D3/D6).

## 4. Fleet statuses (proposed model)

The plan prices billable time by rate tier (operating, standby with crew, standby without crew, repair, moving, force majeure). Those are DAY RATE tiers inside a contract. The rig-level status is a different, shorter list about the rig itself:

| Status | Meaning (proposed) |
|--------|--------------------|
| Operating | under contract, on a well |
| Standby | under contract, waiting (with or without crew is a billing tier, not a rig status) |
| Moving | between locations |
| Stacked | no contract, crew released, preserved |
| Unmapped | records incomplete - the 5 unmapped rigs start here |
| Retired | sold, scrapped or permanently out of the fleet |

OPEN QUESTION for the owner: the exact status list his company uses today. The baseline template (D6) collects this; the list above is a starting proposal and will be corrected to match his practice, not the other way round.

## 5. Status events, not edits

- A status change is an EVENT with an effective date, who entered it, and an optional note. The register's current_status is derived from the latest event, never edited in place.
- Full history is kept: when a rig went stacked, for how long, when it came back. This history feeds fleet planning and, later, R4 analytics.
- Entry rule (until D1 lands): operations proposes the change, operations manager approves. Everything is audited either way.

## 6. Permissions

- Rig roles see only their own Rig_ID (ERPNext User Permissions) - mostly irrelevant for the register itself, which is fleet-level reference data readable by all internal users.
- Only operations (propose) and operations manager (approve) can write status events.
- The register holds no personal data. Rig crew assignments belong to Frappe HR (R2), not here.

## 7. Data model (Frappe DocTypes, proposed)

- `Rig` - the register record (section 3 fields).
- `Rig Status Event` - rig_id, status, effective_date, entered_by, approved_by, note. Immutable once approved; corrections are new events.
- Client and Contract are separate DocTypes in the R1 contract register (DD-06); the register links to them.

## 8. Migration and baseline

- Source: the owner's Excel records (not yet received - D3/D6).
- Stage 1 loads the five-rig baseline with DUMMY values (per the Stage 1 rule: no real client terms on the test server).
- Real migration happens after D3 confirms what the records hold; the register is the first thing loaded because everything else links to it.

## 9. Acceptance for this design

- The owner can see every rig, its status and its status history on one screen.
- A status change takes under a minute to enter and approve.
- A dummy 13th rig is added with settings only, no code.
- Every field in section 3 is either populated from the Excel records or explicitly marked "no source - kept empty".

## 10. What this document needs from the owner

1. The Excel records (rig list, statuses as used today) - decisions D3/D6.
2. Confirmation or correction of the status list in section 4.
3. Pilot rig candidates, when ready (D7) - the register is loaded pilot-first.
