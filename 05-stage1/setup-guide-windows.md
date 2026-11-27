# Stage 1 test server: setup guide for a Windows office machine

For: the owner's IT person (or the owner himself). Time: about 1-2 hours, mostly downloads.
Verified November 27, 2026 against the official sources listed at the end.
Golden rules (plan v3.8): DUMMY DATA ONLY - no personal data, no real client contract terms. No rig is connected. Nothing is exposed to the internet. No passwords are ever sent through chat.

## 0. Check the machine first (5 minutes)

Minimum hardware (from Docker's official requirements plus what ERPNext needs to feel usable):

| Check | Minimum | Comfortable |
|-------|---------|-------------|
| RAM | 8 GB | 16 GB |
| CPU | 64-bit, 4 cores, with SLAT | 6+ cores |
| Free disk | 25 GB | 50 GB |
| Windows | Windows 10 22H2 (build 19045) or Windows 11 23H2 (build 22631), 64-bit | Windows 11 current |
| Virtualization | ENABLED in BIOS/UEFI | same |

How to check virtualization: Task Manager -> Performance -> CPU -> "Virtualization: Enabled". If it says Disabled, enable Intel VT-x / AMD-V in the machine's BIOS/UEFI first; nothing below works without it.

## 1. Why Docker + WSL2 (the verified path)

- Frappe officially supports Linux and macOS only. Its own installation docs say: Windows users should use Ubuntu in WSL.
- Docker Desktop on Windows uses the WSL 2 backend by default and needs no admin rights for the recommended per-user install.
- frappe_docker is the OFFICIAL container setup for Frappe/ERPNext, and its demo file (pwd.yml) currently ships ERPNext v16.61.0 on MariaDB 11.8 - matching the plan.
- Containers keep the whole test server in one folder, easy to wipe and rebuild. That suits a throwaway-grade test server.

## 2. Install WSL2 (10 minutes, one reboot)

Open PowerShell as Administrator:

```powershell
wsl --install
wsl --update
wsl --version
```

Reboot when asked. `wsl --version` must show 2.1.5 or later.

## 3. Install Docker Desktop (15 minutes)

1. Download Docker Desktop for Windows from docker.com (official).
2. Install with defaults (WSL 2 backend, per-user install - no admin needed).
3. Start Docker Desktop and wait for "Engine running".

Verify in PowerShell:

```powershell
docker --version
docker compose version
```

## 4. Get the official Frappe Docker files (5 minutes)

```powershell
cd C:\
mkdir stage1
cd stage1
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
```

(If git is missing: install "Git for Windows" from git-scm.com, or download the repo as a ZIP from github.com/frappe/frappe_docker and extract it.)

## 5. Start the test server (20-40 minutes, mostly downloads)

```powershell
docker compose -f pwd.yml up -d
```

This pulls the images (several GB on first run) and builds a ready ERPNext v16 site called `frontend`.

Watch the site-creation step finish:

```powershell
docker compose -f pwd.yml logs -f create-site
```

When it stops logging and exits, the site is ready.

## 6. First login

- Open http://localhost:8080 on the same machine.
- User: `Administrator`   Password: `admin`
- Change the Administrator password right away, even though this is a test machine.

Other machines in the office can reach it at http://<machine-ip>:8080 on the LAN only. Do NOT forward any port on the router, and do NOT expose the machine to the internet.

## 7. What goes on it

- The five-rig baseline with DUMMY rig names, dummy client names and dummy day rates (we provide the file when DD-01 is approved).
- Nothing real: no crew names, no client contracts, no invoices.

## 8. Stop / wipe / rebuild

```powershell
docker compose -f pwd.yml down            # stop
docker compose -f pwd.yml down -v         # wipe EVERYTHING including the database
```

Wiping is safe: dummy data only, and rebuild is step 5 again.

## 9. If Docker is a problem: the alternative

Frappe's docs also support installing Ubuntu under WSL2 and running bench natively (MariaDB 11.8, Python 3.14, Node 24, Redis per the v16 prerequisites). It works, but it is more moving parts on a Windows office machine. Use it only if Docker Desktop cannot run (for example, virtualization cannot be enabled).

## 10. Support from us

We do not remote into the machine and we never ask for passwords in chat. If the owner later wants us to operate a server directly, the safe route is: a server (cloud VM or this machine) whose login he saves through a vault link we send him - the password is typed only into that page, never into a chat. That is his choice, and it is not needed for Stage 1: this guide is enough for his IT person to run it.

## Sources (checked Nov 27, 2026)

- Frappe installation (Windows via WSL; v16 prerequisites: MariaDB 11.8, Python 3.14, Node 24): https://docs.frappe.io/framework/user/en/installation
- frappe_docker (official container setup; pwd.yml demo): https://github.com/frappe/frappe_docker
- pwd.yml (ERPNext v16.61.0, MariaDB 11.8, site `frontend`, admin/admin): https://raw.githubusercontent.com/frappe/frappe_docker/main/pwd.yml
- Docker Desktop for Windows requirements (WSL 2.1.5+, Windows 10 22H2 / 11 23H2, 8GB RAM, SLAT, virtualization): https://docs.docker.com/desktop/setup/install/windows-install/
