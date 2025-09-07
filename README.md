
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

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/6912ce10810e381fea4def8ba94e44a931b9fa24/Screenshot%202025-09-06%20184735.png)

**Patching**- Update and upgrades are done on the Linux VM

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/3f56e6ce6a4b9c861f2f8ab1c32d5f70cb8b1a5b/Screenshot%202025-09-06%20184841.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/56666c704cba992196411cb5e1b83393f28becd7/Screenshot%202025-09-06%20185126.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/f87de789157b2161344abad54e98d56b08272097/Screenshot%202025-09-06%20185238.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/6dfb652cc38762983f45421e0f0f4443f75edde3/Screenshot%202025-09-06%20185319.png)

2. **Explore filesystem** to identify config and log directories (`ls`, `tree`, `df`).

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/997159adafc606d236bc509bc5822286e380cf13/Screenshot%202025-09-06%20192959.png)

Installation of tree in the Linux VM

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/9193c62f751b443e2d771c589d89ec5ab3023be3/Screenshot%202025-09-06%20193243.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/dd2e12679800e5af313707b9f80dc3bc67e2925b/Screenshot%202025-09-06%20195206.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/598bc2f9902d1a91af90789f7697958b77869fb1/Screenshot%202025-09-06%20195235.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/d9ded6a5825fdb83a11f030f89edb4b983997b65/Screenshot%202025-09-06%20195716.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/18c2e292dcbb06a4dbf758394f69e40b5aa3ddab/Screenshot%202025-09-06%20195832.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/c8776ad6a513181d9c2a13beb538a6e31cddd086/Screenshot%202025-09-06%20200132.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/4e5069ba6dfa1bd52de58fe41f0a8bf34cff4028/Screenshot%202025-09-06%20200247.png)
   
3. **Create users and groups** (`useradd`, `groupadd`, `usermod`, `chmod`, `chown`) following least privilege.

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/093f70dc0158f86a2f236894b2fcc87464c2e540/Screenshot%202025-09-06%20201635.png)

4. **Harden SSH**: change port, disable root login, enforce key-based auth.

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/5bded1d4624e6aa5ec893d1b21eb7f3afd3dea79/Screenshot%202025-09-06%20202957.png)

![image alt](https://github.com/GodwinChineduNedu/Secure-Linux-Server-Setup-Audit/blob/142a44a4fbaaf93e9bf3ce9bc63d73cbdfce4f98/Screenshot%202025-09-06%20203224.png)

8. **Install Nginx** and confirm it serves a default test page.
9. **Automate backups** with a Bash script (`etc_backup.sh`) to archive `/etc` configs to `/var/backups/etc`, scheduled via cron.
10. **Monitor logs** (`/var/log/auth.log`, `/var/log/syslog`) for failed logins and system events.
11. **Generate an audit report** with `uname`, `df`, `free`, `ps aux`, `ss -tuln` into `audit_report.txt`.
12. **Push project** files (scripts, README, reports, optional screenshots) to GitHub for portfolio use.

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

















