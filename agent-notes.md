# Agent Notes - Internal Ticket Troubleshooting Log

> These are internal agent notes documenting the troubleshooting steps taken for all 3 simulated helpdesk tickets. These notes were posted inside each ticket thread in osTicket and are not visible to end users.

---

## TKT-934763 — Password Reset (Sev-2 High)

**Submitted by:** Raymond Mathews — Finance Department  
**Assigned to:** Tidal Banks — IT Support  
**SLA:** Sev-2 High — 4 hour response  

```
[Internal Note — Agent: Tidal Banks | 12:45]


12:45 — Ticket received and acknowledged. User reports inability

to log in. Account locked confirmed in admin panel.

12:55 — Contacted user via phone to verify identity. Confirmed

full name and employee ID before proceeding.

13:00 — Logged into Microsoft 365 Admin Center. Located user

account under Active Users. Sign-in status showed as blocked

due to 5 consecutive failed login attempts.

13:15 — Unblocked sign-in and initiated password reset. Enabled

"require password change on next sign-in" option.

13:20 — Communicated temporary password to user securely via

phone. User confirmed successful login and changed password.

13:25 — Verified email and system access restored. Ticket closed.

Resolution time: 25 minutes. Within Sev-2 SLA (4 hours).
```

---

## TKT-481127 — Can't Access Shared Drive (Sev-3 Normal)

**Submitted by:** Bernard Muzeki — Finance Department  
**Assigned to:** Tidal Banks — IT Support  
**SLA:** Sev-3 Normal — 8 hour response  

```
[Internal Note — Agent: Tidal Banks| 20:00]

20:00 — Ticket received. User reports shared drive showing
as unavailable since this morning with no changes on their end.

20:05 — Asked user to confirm whether the issue affects only
them or the entire team. User confirmed it's individual only.
Ruled out a server-side outage.

20:10 — Remoted into user's workstation. Checked drive mapping
under File Explorer → This PC. Shared drive path was missing
from the mapped drives list entirely.

20:15 — Checked user's group membership in Microsoft 365
Admin Center → Active Users → [User] → Groups tab.
Confirmed user was missing from the Finance-Staff security
group which controls shared drive access permissions.

20:20 — Re-added user to Finance-Staff security group.
Asked user to sign out and sign back in to refresh
group policy and access tokens.

20:30 — User confirmed shared drive is now visible and
fully accessible. Drive path confirmed as \\server\finance.

20:35 — Root cause documented as accidental group membership
removal during a recent admin group policy update.
Ticket closed. Resolution time: 35 minutes.
Within Sev-3 SLA (8 hours). ✅
```

---

## TKT-304502 — New Employee Account Setup (Sev-3 Normal)

**Submitted by:**  Lisa Madison HR Department  
**Assigned to:** Makanaka Mutize — Systems Admin  
**SLA:** Sev-3 Normal — 8 hour response  

```
[Internal Note — Agent: Makanaka Mutize| 7:53]

11:00 — Ticket received from HR requesting new user account
provisioning for incoming employee Jane Smith joining the
Finance Department on [start date].

11:05 — Confirmed required details with HR contact:
  - Full name: Jane Smith
  - Job title: Finance Officer
  - Department: Finance
  - Start date: [DD/MM/YYYY]
  - Required software: Microsoft 365, shared drive access

11:15 — Logged into Microsoft 365 Admin Center.
Created new user account:
  - Display name: Jane Smith
  - Username: jane.smith@[domain]
  - Department: Finance
  - License: Microsoft 365 Business Basic assigned

11:25 — Added Jane Smith to the Finance-Staff security
group to grant shared drive access permissions.

11:30 — Added user to Microsoft Teams and Finance
Department channel for team communication.

11:35 — Enabled Multi-Factor Authentication (MFA) on the
new account as per company security policy.

11:40 — Set password to expire on first login.
Sent welcome email to HR with Jane's temporary credentials
and first login instructions. Advised HR to share credentials
with new employee securely in person.

11:45 — All systems provisioned and ready for start date.
Ticket closed. Resolution time: 45 minutes.
Within Sev-3 SLA (8 hours). ✅
```

---

*Agent notes created as part of Lab 2 — osTicket Helpdesk Deployment home lab.*
