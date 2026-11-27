# DD-02: Daily drilling report, client sign-off and locking

Status: DRAFT v0.1 (Nov 27, 2026) - for owner review. Nothing here is built; production code waits for the owner's design approval.
Release: R1. Feeds: acceptance criteria (section 6 of the plan), D8, D10, D12; legal review under Law 6/2022.
This document collects every signature rule settled across plan v3.7 into one design.

## 1. Purpose

The daily drilling report is the commercial heart of R1: the client signs it, billing prices from it, and disputes are settled against it. It must work offline on a rig tablet for seven days, in Arabic and English, and a signed report must be provable in a billing dispute years later.

## 2. Report content (structure, fields filled per rig-day)

- Header: Rig_ID (DD-01), date, well, client, contract, report number (sequential per rig).
- Time breakdown in hours against the contract's rate tiers: operating, standby (with/without crew), repair, moving, force majeure, lost time with reason codes.
- Work summary: free text, bilingual (Arabic right-to-left and English, both layouts from day one).
- Disputed lines: the company man can flag a lost-time line as disputed AT SIGN-OFF instead of refusing the whole report; disputed lines flow to a dispute state and back.
- Attachments: photos, BOP test references (records only - the AI never touches BOP systems).

## 3. The signature (the design that makes it real)

Per-signer keys:
- Each signer (rig-side company representative AND the client company man) gets his own key pair at enrollment.
- The private key is generated inside the tablet's secure hardware and never leaves it. Android key attestation is verified at enrollment, so this is PROVEN per device, not assumed. Note: ATEX/IECEx-rated tablets may offer TEE but not StrongBox - confirmed per model before purchase (D13).
- The key unlocks with the signer's PIN. Wrong-PIN attempts are limited (proposed: 5), after which the key locks and the device requires re-enrollment; a lost tablet is remotely wiped (D13) - see section 6 for the wipe trade-off.

What is signed:
- The report is serialized in ONE canonical format before signing: fixed field order, fixed number formats, defined Arabic text handling (normalization), defined attachment hashing. Honest re-saves then never fail verification. The canonical format is specified in this document's appendix A (to be written during design - it is a formatting spec, not a decision).
- The device signs the canonical report's hash with a timestamp. The server verifies against the signer's registered public key on sync. An edited report fails verification even if the editor recomputes the hash.

Counterparty copy (the dispute-settler):
- The moment the company man signs, the signed canonical report plus the signature go to the OPERATOR'S own address (email or operator portal). An independent copy the contractor cannot touch is what actually settles "you signed for him" arguments.

Provenance and custody:
- Every signature records which app build produced it (build pinning).
- The operator confirms each of its signers' keys in writing at enrollment.
- An e-signature clause joins the drilling contract or a side letter (contracts/legal, with D16's contract-by-contract check).
- Lawyer questions (open items): whether the tablet signature holds for invoicing under Law 6/2022's electronic-signature chapter, and whether a licensed certification provider is required for full legal weight.

Key lifecycle:
- Revocation and re-issue when a company man rotates out; the public-key registry records who held which key when, so old signatures stay verifiable.

## 4. Locking and amendments

- A signed report is LOCKED. No edit, by anyone, including administrators.
- A correction is a new AMENDMENT document: it references the signed report, carries its own reason, and is signed again by the same roles. The original is never overwritten; the amendment chain is the audit trail.
- Billing always reads the latest signed state (report plus amendments).

## 5. Offline behaviour

- Reports queue on the tablet with unique IDs for up to seven days (D8 prototype P1 proves this on a real rugged tablet).
- Signatures happen offline against the on-device key; verification happens on sync.
- Conflicts (head office edited a record while the rig was offline) follow the D12 policy per document type; device time and server receipt time are both stored.
- Sync-health targets per rig are measured from the pilot.

## 6. The remote-wipe trade-off

Remote wipe protects client-signed data on a lost tablet but destroys up to seven days of unsynced signed reports, which would break the no-lost-records rule. Fallback (D12):
- Proposed: a second registered tablet per rig, or a paper report signed the same day, with a defined re-entry and re-signing procedure on the replacement device.
- The re-entry rule: re-entered reports are marked as such, reference the lost device's queue, and are signed fresh; they never silently replace the originals.

## 7. Who can do what (until D1 lands)

| Action | Rig clerk | Rig manager | Company man | Operations |
|--------|-----------|-------------|-------------|------------|
| Draft report | yes | yes | no | yes |
| Sign (rig side) | no | yes | no | no |
| Sign (client side) | no | no | yes | no |
| Flag dispute | no | no | yes | no |
| Approve amendment | no | yes | yes (re-sign) | yes |
| See other rigs | no | no | own contract/well only | yes |

The company man signs through a restricted outside account scoped to his contract and well.

## 8. Acceptance tests this design must pass (plan section 6)

- Daily reports done in the system for the last four weeks of the pilot, with client sign-off, spot-checked against the paper copy.
- Signed reports locked; corrections create signed amendments.
- Tamper test: any post-signature edit fails verification.
- Offline test: seven days queued on a rugged tablet, then sync with no lost, doubled or misfiled records (prototype P1 first).
- Dispute flow: a flagged lost-time line moves to dispute and back, with billing reading the resolution.

## 9. Open items

1. Appendix A: the canonical format specification (written during design, before P3).
2. Wrong-PIN limit (proposed 5) and re-enrollment procedure - confirm with operations.
3. Fallback choice: second tablet vs same-day paper (D12, with operations).
4. Lawyer answers on Law 6/2022 (open items list).
5. Report number scheme per rig - confirm against current practice from the Excel records.
