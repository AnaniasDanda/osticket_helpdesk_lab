# SLA & Departments Configuration Reference

> This document outlines the helpdesk configuration set up in osTicket for Lab 2. It serves as a handover reference to the kind of documentation provided to a colleague or manager in a real IT environment.

---

## Departments

| Department    | Purpose                                              | Manager        |
|---------------|------------------------------------------------------|----------------|
| IT Support    | First-line support  password resets, access issues, software problems | Ananias Danda |
| Systems Admin | User provisioning, account setup, server-related tasks | Ananias Danda |
| Network       | Connectivity issues, network access, infrastructure  | Ananias Danda |

---

## SLA Plans

| SLA Plan        | Response Time | Schedule       | Use Case                                      |
|-----------------|---------------|----------------|-----------------------------------------------|
| Sev-1 Critical  | 1 hour        | 24/7           | Full system outage, security breach, critical data loss |
| Sev-2 High      | 4 hours       | 24/7           | User fully locked out, key system unavailable |
| Sev-3 Normal    | 8 hours       | Business hours | General requests, non-urgent access issues, new setups |

---

## Help Topics

| Help Topic                  | Default Department | Default SLA    |
|-----------------------------|-------------------|----------------|
| Password Reset              | IT Support        | Sev-2 High     |
| Software Issue              | IT Support        | Sev-3 Normal   |
| Hardware Failure            | IT Support        | Sev-2 High     |
| New User Access Request     | Systems Admin     | Sev-3 Normal   |
| Network Connectivity        | Network           | Sev-2 High     |

---

## Agent Accounts

| Agent Name    | Department         | Role        | Access Level |
|---------------|--------------------|-------------|--------------|
| Ananias Danda   | IT Support         | Admin       | All Access   |
| Makanaka Mutize      | Systems Admin      | Agent       | All Access   |
| Raji Mutazu       | Network            | Agent       | All Access   |

> All agents were also granted Extended Access to all other departments to ensure visibility of all tickets during this lab simulation.

---

## Access URLs

| Portal       | URL                              | Who Uses It          |
|--------------|----------------------------------|----------------------|
| End User     | http://localhost/osticket        | Staff submitting tickets |
| Agent Panel  | http://localhost/osticket/scp    | IT agents managing tickets |
| Admin Panel  | http://localhost/osticket/scp (toggle top right) | Admin configuration |

---

*Configuration reference created as part of Lab 2 — osTicket Helpdesk Deployment home lab.*
