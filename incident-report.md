# Incident Report IT Helpdesk Ticket

---

## Ticket Summary

| Field             | Details                            |
|-------------------|------------------------------------|
| **Ticket ID**     | TKT-934763                          |
| **Date Opened**   | 13/05/2026                       |
| **Date Closed**   | 13/05/2026                       |
| **Time to Close** | [e.g. 3 hours 15 minutes]          |
| **Submitted By**  | Raymond Mathews (End User)                |
| **Assigned To**   | Tidal banks (IT Support Agent)     |
| **Department**    | IT Support                         |
| **Help Topic**    | Password Reset                     |
| **SLA Tier**      | Sev-2 High — 4 hour response       |
| **Priority**      | High                               |
| **Status**        | Resolved ✅                        |

---

## 1. Incident Description

The user John Doe submitted a ticket reporting that he was unable to log into his workstation after returning from a two-week leave. The system was displaying an "Account Locked" error message and he was unable to access any company resources including email and shared drives.

---

## 2. Impact Assessment

| Area             | Impact                                               |
|------------------|------------------------------------------------------|
| **User Affected** | 1 (Raymond Mathews — Finance Department)                  |
| **Systems Affected** | Workstation login, Email (Microsoft 365), Shared Drive access |
| **Business Impact** | User unable to perform daily tasks                |
| **Urgency**       | High — active business hours, user fully locked out |

---

## 3. Root Cause

The user's account had been automatically locked by the system's security policy due to **5 consecutive failed login attempts** prior to his leave period. The account lockout policy is set to lock accounts after 5 failed attempts with no automatic unlock timer, requiring manual intervention by an IT administrator.

---

## 4. Troubleshooting Steps

**Step 1 — Ticket acknowledgement**
- Received ticket notification in the osTicket agent panel
- Assigned ticket to IT Support department under Sev-2 SLA
- Sent acknowledgement reply to user confirming ticket receipt and estimated response time

**Step 2 — Identity verification**
- Contacted the user via phone to verify identity before making any account changes
- Confirmed full name, employee ID, and department as per company security policy

**Step 3 — Account investigation**
- Logged into the Microsoft 365 Admin Center
- Navigated to Users → Active Users → searched for John Doe
- Confirmed the account was present and licensed but showed sign-in blocked status
- Reviewed the sign-in logs — confirmed 5 failed login attempts on [date] at [time]

**Step 4 — Account unlock and password reset**
- Unblocked the user's sign-in under Active Users → Manage sign-in status
- Initiated a password reset and set the option to require the user to change password on next sign-in
- Communicated the temporary password to the user securely via phone (not email)

**Step 5 — Verification**
- Confirmed with the user that he was able to log in successfully with the temporary password
- User successfully changed their password on first login
- Verified email access and shared drive access were restored

**Step 6 — Ticket closure**
- Added internal resolution note to the ticket documenting all steps taken
- Closed the ticket with a resolution summary visible to the user
- Sent a follow-up message to the user confirming resolution and advising them to contact IT if further issues arose

---

## 5. Resolution

The user's account was unlocked in the Microsoft 365 Admin Center and a password reset was issued. The user successfully logged in and regained full access to all systems within the SLA response window.

---

## 6. Preventive Recommendations

| Recommendation | Details |
|----------------|---------|
| **User awareness** | Advise users to notify IT before extended leave so accounts can be monitored or temporarily suspended cleanly |
| **Lockout policy review** | Consider configuring an automatic unlock timer (e.g. 30 minutes) for lower risk lockouts to reduce helpdesk load |
| **Self-service password reset** | Evaluate enabling Microsoft 365 Self-Service Password Reset (SSPR) to allow users to unlock their own accounts securely |

---

## 7. Lessons Learned

- Always verify user identity before making any account changes even for low risk requests like password resets
- Documenting every step taken during a ticket resolution creates an audit trail and helps future agents handle similar issues faster
- Checking sign-in logs before making changes helps confirm the root cause rather than assuming

---

## 8. Agent Sign-Off

| Field         | Details              |
|---------------|----------------------|
| **Agent Name** | Tidal banks   |
| **Role**       | IT Support Agent    |
| **Date**       | 13/05/2026       |

---

*This incident report was created as part of a self-directed IT Support & Systems Administration home lab using osTicket deployed on UTM (macOS).*
