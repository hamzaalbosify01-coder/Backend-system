# Design document index

The design phase produces this numbered set before any production code (owner-kept limit, November 27, 2026). Each document is reviewed and approved by the owner before build starts on its release. Status: Planned / Draft / In review / Approved.

| ID | Design document | Release | Feeds decisions | Status |
|----|-----------------|---------|-----------------|--------|
| DD-01 | Rig register, permanent Rig_ID keys and fleet statuses | R1 | D6 | Draft v0.1 (Nov 27), awaiting owner review |
| DD-02 | Daily drilling report with client sign-off (per-signer keys, canonical format, locking, amendments) | R1 | D10 | Draft v0.1 (Nov 27), awaiting owner review |
| DD-03 | Approvals and audit trail (matrix per document type) | R1 | D1 | Planned |
| DD-04 | Offline capture and sync (tablet app vs ODK, queue, conflict policy) | R1 | D8, D12, D2 | Planned |
| DD-05 | Permissions and row-level security (read-replica reporting model) | R1 | D1 | Planned |
| DD-06 | Fleet and contract planning workspace | R1 | - | Planned |
| DD-07 | Data migration and cleanup (from the Excel records) | R1 | D3 | Planned |
| DD-08 | Equipment, maintenance triggers and ISO 14224 failure coding | R1b | - | Planned |
| DD-09 | Invoicing and accounting cutover | R1b | D15 | Planned |
| DD-10 | HR, crews, certificates and Libyan payroll (Frappe HR) | R2 | - | Planned |
| DD-11 | AI copilot (hosting, permission tests, proposal writes, observability) | own track | D4, D14 | Planned |
| DD-12 | Rig data link (WITS0 collector, data diode, IEC 62443) | R3 | D16 | Planned |
| DD-13 | Security architecture (OWASP ASVS 5.0 L2, pen-test plan, recovery) | all | - | Planned |
| DD-14 | Tablet fleet management (Android Enterprise / Headwind MDM) | R1 | D13 | Planned |

First to be drafted: DD-01 (register and statuses), because every other document keys off Rig_ID.
