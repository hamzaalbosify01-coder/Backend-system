# Stage 1: test server

Purpose: a throwaway-grade test server where the owner reviews real screens (rig register, statuses) before anything else is built. Approved under the November 27 working framework (Stage 0/1 setup is delegated; spending is not).

Rules (from plan v3.7):
- Small cloud VM or an existing local machine - nothing is ordered or paid without the owner's approval.
- Holds NO personal data and NO real client contract terms: the five-rig baseline loads with dummy names, rates and terms.
- No rig is connected. No production anything.

Planned stack: Frappe + ERPNext v16 (official frappe_docker), MariaDB with point-in-time recovery configured from day one (practice for the real thing), HTTPS off (internal only) until D5 decides where the real system lives.

Setup steps land here as a script once the host is chosen - choosing the host is the only thing waiting on the owner (a small cloud VM costs roughly $5-$15/month at this size; existing office hardware costs nothing).
