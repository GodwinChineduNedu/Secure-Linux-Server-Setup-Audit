
#  Secure Linux Server Setup & Audit

---

## Business Goal

A small startup needs to deploy a Linux-based web application server in the cloud.  
They want:

- A **secure** baseline (no default passwords, no open ports).
- A **repeatable** process (documented steps, scripts).
- The ability to **audit** the server state at any time.

This project demonstrates how to build such a server from scratch, harden it, deploy a basic service, and produce an audit report — just like a junior DevOps/Cloud Security engineer would in production.

---

##  Architecture Overview

```text
┌──────────────┐
│ Developer PC │
└──────┬───────┘
       │ SSH (Port 2222)
┌──────▼────────┐      ┌───────────┐
│ Cloud VM (OS) │◄────►│ Nginx Web │
│ Ubuntu Linux  │      │ Service   │
└───────────────┘      └───────────┘
````

* **Cloud VM**: Single Linux instance (could be AWS, GCP, Azure, or local VM).
* **Secure SSH**: Non-default port, no root login, key-based authentication.
* **Service**: Nginx serving a test page.
* **Backup and Audit**: Automated scripts and log analysis.

---

##  Tools Used and Why

| Tool / Service        | Purpose                                  | Why It Was Chosen                               |
| --------------------- | ---------------------------------------- | ----------------------------------------------- |
| Ubuntu Server (Linux) | Host operating system                    | Common in production; stable and well supported |
| SSH                   | Secure remote access                     | Industry standard for remote admin              |
| Nginx                 | Web service                              | Lightweight, reliable web server                |
| Bash / Shell scripts  | Automation (backups, user creation)      | Universal in Linux environments                 |
| Cron                  | Task scheduling                          | Simple, native automation                       |
| Git & GitHub          | Version control and portfolio publishing | De-facto standard for DevOps sharing            |
| `tree`, `ls`, `df`    | Filesystem exploration                   | Quick visibility into system state              |
| `tar`                 | Archiving backups                        | Common backup format                            |
| `tail`, `less`        | Log monitoring                           | Real-time and on-demand log review              |

---

##  Step-by-Step Build Process

1. **Provision** a Linux VM (cloud or local).
2. **Explore filesystem** to identify config and log directories (`ls`, `tree`, `df`).
3. **Create users and groups** (`useradd`, `groupadd`, `usermod`, `chmod`, `chown`) following least privilege.
4. **Harden SSH**: change port, disable root login, enforce key-based auth.
5. **Install Nginx** and confirm it serves a default test page.
6. **Automate backups** with a Bash script (`etc_backup.sh`) to archive `/etc` configs to `/var/backups/etc`, scheduled via cron.
7. **Monitor logs** (`/var/log/auth.log`, `/var/log/syslog`) for failed logins and system events.
8. **Generate an audit report** with `uname`, `df`, `free`, `ps aux`, `ss -tuln` into `audit_report.txt`.
9. **Push project** files (scripts, README, reports, optional screenshots) to GitHub for portfolio use.

---

##  Screenshots / CLI Outputs

> *(Replace with your actual screenshots or terminal captures)*

Example CLI output:

```bash
$ uname -a
Linux secure-server 5.15.0-89-generic #99-Ubuntu SMP x86_64 GNU/Linux

$ ss -tuln
Netid State  Recv-Q Send-Q Local Address:Port Peer Address:Port
tcp   LISTEN 0      128         0.0.0.0:80    0.0.0.0:*
tcp   LISTEN 0      128         0.0.0.0:2222  0.0.0.0:*
```

Backup files created:

```bash
$ ls /var/backups/etc
etc_backup_2025-09-06_02-00-00.tar.gz
etc_backup_2025-09-07_02-00-00.tar.gz
```

---

##  Lessons Learned

* **Planning matters**: mapping out steps before touching the server reduces mistakes.
* **Small changes improve security a lot**: disabling root SSH and changing the port cut down brute-force attempts.
* **Automation saves time**: a 3-line Bash script plus cron is enough to protect configs.
* **Documentation is valuable**: clear notes and audit reports help future engineers (or your future self).
* **Version control makes it portable**: pushing to GitHub makes this reusable and demonstrates professional practice.

---

