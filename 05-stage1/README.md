# Stage 1: test server

Purpose: a throwaway-grade test server where the owner reviews real screens (rig register, statuses) before anything else is built. Approved under the November 27 working framework (Stage 0/1 setup is delegated; spending is not).

Rules (from plan v3.7):
- Small cloud VM or an existing local machine - nothing is ordered or paid without the owner's approval.
- Holds NO personal data and NO real client contract terms: the five-rig baseline loads with dummy names, rates and terms.
- No rig is connected. No production anything.

Planned stack: Frappe + ERPNext v16 (official frappe_docker), MariaDB with point-in-time recovery configured from day one (practice for the real thing), HTTPS off (internal only) until D5 decides where the real system lives.

Host chosen by the owner (Nov 27): an existing office machine running Windows - no spending.
The step-by-step guide for his IT person is setup-guide-windows.md in this folder (Docker Desktop with the WSL2 backend plus the official frappe_docker demo setup, ERPNext v16.61.0). Hardware to check first: 8GB RAM (16 better), 4-core 64-bit CPU with SLAT, virtualization enabled in BIOS, 25GB free disk, Windows 10 22H2+ or 11 23H2+.
