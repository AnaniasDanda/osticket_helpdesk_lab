# Lab 2 : IT Helpdesk Ticketing System  osTicket Deployment

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Platform](https://img.shields.io/badge/platform-Ubuntu%2022.04%20ARM64-orange)
![Hypervisor](https://img.shields.io/badge/hypervisor-UTM-red)
![Stack](https://img.shields.io/badge/stack-LAMP-blue)
![Tool](https://img.shields.io/badge/tool-osTicket%20v1.18-purple)
![Host](https://img.shields.io/badge/host-macOS%20Apple%20Silicon-black)

---

## Overview

This lab simulates a real world IT helpdesk environment by deploying and configuring **osTicket**,an open source ticketing system on a self hosted Ubuntu Server virtual machine running inside **UTM on macOS**. The goal was to demonstrate practical skills in Linux server administration, LAMP stack deployment, helpdesk configuration, and end to end IT service management (ITSM) workflows including ticket submission, assignment, resolution, and formal incident documentation.

---

## Repository Structure

```
osticket-helpdesk-lab/
│
├── README.md                        ← You are here
├── incident-report.md               ← Mock incident report (Ticket TKT-0002)
├── agent-notes.md                   ← Internal troubleshooting notes for all 3 tickets
├── sla-and-departments-config.md    ← SLA tiers and department structure reference
│
└── screenshots/
    ├── 01-utm-vm-setup.png
    ├── 02-mysql-database-created.png
    ├── 03-osticket-installer-success.png
    ├── 04-admin-panel-dashboard.png
    ├── 05-sla-plans-config.png
    ├── 06-help-topics-config.png
    ├── 07-agent-accounts.png
    ├── 08-ticket-submitted.png
    ├── 09-open-ticket-queue.png
    ├── 10-ticket-assigned-to-agent.png
    ├── 11-internal-agent-notes.png
    └── 12-resolved-tickets-view.png
```

---

## Environment

| Component      | Details                           |
|----------------|-----------------------------------|
| Host Machine   | macOS (Apple M-series)            |
| Hypervisor     | UTM (Apple Silicon)               |
| OS             | Ubuntu Server 22.04 LTS (ARM64)   |
| Web Server     | Apache 2                          |
| Database       | MySQL 8.0                         |
| Language       | PHP 8.1                           |
| Ticketing App  | osTicket v1.18.1                  |
| Network        | UTM Shared Network + Port Forward |

---

## What I Built

- Provisioned an Ubuntu Server 22.04 ARM64 VM from scratch in UTM on macOS
- Installed and configured a full LAMP stack (Linux, Apache, MySQL, PHP)
- Resolved MySQL password policy and privilege errors during database setup
- Deployed osTicket via the web installer and secured the installation post-setup
- Configured the helpdesk admin panel with:
  - **3 Departments:** IT Support, Systems Admin, Network
  - **3 SLA Tiers:** Sev-1 Critical (1hr/24-7), Sev-2 High (4hr/24-7), Sev-3 Normal (8hr/business hours)
  - **5 Help Topics:** Password Reset, Software Issue, Hardware Failure, New User Access Request, Network Connectivity
  - **3 Agent Accounts** with role based department access (All Access)
- Submitted 3 mock tickets as end users through the user portal
- Assigned tickets to agents and departments through the agent panel
- Documented internal troubleshooting notes for all 3 tickets
- Resolved all tickets and wrote a formal incident report

---

## Skills Demonstrated

- Linux CLI administration (package management, file permissions, service control)
- LAMP stack deployment and configuration from scratch
- MySQL database creation, user management, and privilege assignment
- Web application deployment and post install security hardening
- ITSM concepts: SLA tiers, ticket lifecycle, department routing, escalation
- Role-based access control (RBAC) for helpdesk agents
- IT documentation: internal agent notes and formal incident reporting

---

## Deployment Walkthrough

### 1. VM Setup in UTM

Created an Ubuntu Server 22.04 LTS (ARM64) VM in UTM. Allocated 2GB RAM and 20GB storage. Configured network as **Shared Network** with port forwarding (TCP Host 80 → Guest 80) so osTicket is accessible from the Mac browser at `http://localhost/osticket`. Enabled OpenSSH during Ubuntu installation for terminal access.

```bash
ip addr show   # Get VM IP address
```

### 2. LAMP Stack Installation

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 -y
sudo apt install mysql-server -y
sudo mysql_secure_installation
sudo apt install php libapache2-mod-php php-mysql php-xml php-mbstring php-intl php-apcu php-gd -y
sudo systemctl restart apache2
```

> **Note:** `php-imap` is optional — only needed for email-to-ticket piping. Not required for this lab.

### 3. MySQL Database Setup

```bash
sudo mysql
```

```sql
DROP DATABASE IF EXISTS osticket;
DROP USER IF EXISTS 'osticket'@'localhost';
CREATE DATABASE osticket;
CREATE USER 'osticket'@'localhost' IDENTIFIED BY 'Pass123!';
GRANT ALL PRIVILEGES ON osticket.* TO 'osticket'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Verify database was created:

```sql
SHOW DATABASES;
```

### 4. osTicket Installation

```bash
cd /tmp
wget https://github.com/osTicket/osTicket/releases/download/v1.18.1/osTicket-v1.18.1.zip
sudo apt install unzip -y
unzip osTicket-v1.18.1.zip -d osticket
sudo cp -r osticket/upload /var/www/html/osticket
sudo chown -R www-data:www-data /var/www/html/osticket
sudo chmod -R 755 /var/www/html/osticket
cd /var/www/html/osticket/include
sudo cp ost-sampleconfig.php ost-config.php
sudo chmod 0666 ost-config.php
```

Ran web installer at `http://localhost/osticket/setup` and completed setup wizard using MySQL credentials.

Post install security:

```bash
sudo rm -rf /var/www/html/osticket/setup
sudo chmod 0644 /var/www/html/osticket/include/ost-config.php
```

### 5. Admin Panel Configuration

Logged into agent panel at `http://localhost/osticket/scp` and configured:

- **Departments** — Admin Panel → Agents → Departments
- **SLA Plans** — Admin Panel → Manage → SLA
- **Help Topics** — Admin Panel → Manage → Help Topics
- **Agents** — Admin Panel → Agents → Add New (assigned All Access role to all departments)

### 6. Ticket Simulation

Submitted 3 tickets as end users via `http://localhost/osticket`. Logged into the agent panel, viewed the open ticket queue, assigned tickets to agents and departments, posted internal notes, and resolved all tickets with documented resolutions.

---

## SLA Configuration

| SLA Plan        | Response Time | Schedule       |
|-----------------|---------------|----------------|
| Sev-1 Critical  | 1 hour        | 24/7           |
| Sev-2 High      | 4 hours       | 24/7           |
| Sev-3 Normal    | 8 hours       | Business hours |

---

## Ticket Simulation Summary

| Ticket ID  | Issue                        | Department    | SLA Tier | Resolution Time | Status      |
|------------|------------------------------|---------------|----------|-----------------|-------------|
| TKT-248012   | Password Reset               | IT Support    | Sev-2    | 25 minutes      | Resolved ✅ |
| TKT-481127   | Can't Access Shared Drive    | IT Support    | Sev-3    | 35 minutes      | Resolved ✅ |
| TKT-304502  | New Employee Account Setup   | Systems Admin | Sev-3    | 45 minutes      | Resolved ✅ |

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Browser on Mac couldn't reach the VM | Configured UTM port forwarding: Host TCP 80 → Guest 80, accessed via `http://localhost/osticket` |
| MySQL password didn't meet policy criteria | Lowered policy with `SET GLOBAL validate_password.policy = LOW;` before creating user |
| GRANT privileges error on osticket user | Used `DROP USER IF EXISTS` to clear broken user state before recreating cleanly |
| Stuck in MySQL prompt with `'>` indicator | Typed `';` to close open quote then `EXIT;` to return to terminal |
| PHP extensions missing on osTicket install | Installed missing extensions individually: `sudo apt install php-[extension] -y` |
| Config file permission error during install | Set `chmod 0666` on `ost-config.php` before install, locked to `0644` after |
| Ubuntu ISO architecture mismatch | Used ARM64 Ubuntu Server ISO to match Apple Silicon (M-series) chip |
| Tickets not visible in agent panel | Fixed agent role  set Primary Department and all Extended Access departments to **All Access** in Admin Panel → Agents |

---

## Documentation

| File | Description |
|------|-------------|
| [`incident-report.md`](./incident-report.md) | Formal incident report for TKT-0002 (Shared Drive Access) |
| [`agent-notes.md`](./agent-notes.md) | Internal troubleshooting notes for all 3 simulated tickets |
| [`sla-and-departments-config.md`](./sla-and-departments-config.md) | Full SLA and department configuration reference |
| [`images.placeholder.md`](images) | Full Screenshots reference for every step|
---

## Key Takeaways

- Deploying a LAMP stack manually builds a strong foundation for understanding how most enterprise web-based IT tools are hosted and maintained
- osTicket's SLA tiers, department routing, and role based access mirror real enterprise tools like Zendesk, ServiceNow, and Jira Service Management
- File permissions are the most common source of web app deployment failures on Linux understanding `chown` and `chmod` is essential
- MySQL privilege and password policy errors are extremely common in real IT environments — knowing how to troubleshoot them is a practical and valuable skill
- Proper documentation at every step from deployment to ticket resolution is as important as the technical work itself in any IT support role

---

## Tools & Technologies

`Ubuntu Server 22.04` `Apache2` `MySQL 8.0` `PHP 8.1` `osTicket v1.18` `UTM` `macOS` `Linux CLI` `ITSM` `LAMP Stack`

---

*This project was completed as part of a self directed IT Support & Systems Administration home lab series.*

