# Backend-system

Owner repository for the 12-rig drilling-fleet platform (working name: fleet planning and operations platform for a Libyan drilling contractor, 12 rigs, 7 operating).

Everything about this system lives here: decisions, designs, standards, prototypes and plan versions. Never only in a chat, never only on one machine.

## Layout

- `00-governance/` - decision register (D1-D16), approvals log, build limits
- `01-design/` - design documents DD-01 onward, with the index in its README
- `02-standards/` - standards register (editions verified against the publishers)
- `03-prototypes/` - throwaway prototypes under decision D11 guardrails
- `04-plan/` - consolidated plan versions (current: v3.12, November 27, 2026)

## Build limits (owner-kept, November 27, 2026)

- No production code before the owner approves the design.
- No spending without the owner's approval.
- Nothing on production servers or live rigs without the owner.
- No real crew or client data anywhere in this repo or in prototypes.
- The owner keeps: design approvals, every gate signature, lifting the R1 scope freeze, and the choice of the human technical owner, security firm and legal counsel.
- The AI never connects to rig controls, BOP or safety systems. AI proposes; managers approve; nobody approves their own proposal.

## The world-class bar

Verified, gated, secure, safe, recoverable, owned. See plan v3.12, section 6.
