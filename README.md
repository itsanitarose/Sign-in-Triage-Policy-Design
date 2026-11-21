
# Sign-in Triage & Policy Design

<table>
<tr>
<td>

**Case at a Glance**

Reviewed 15 sign-ins against the six rules in place, then designed the rules that should replace them.<BR>
**IAM skills demonstrated:** Sign-in log analysis, risk triage, MFA policy design, and rollout planning.

</td>
</tr>
</table>

<BR>

## 🎫 The Ticket

It's 16 November 2026, my seventh week on the security team at Northwind Health. The company's sign-in rules were set up quickly and have never been revisited. This week's request is to review a day of sign-in activity and propose better rules without locking people out.

My manager writes:

> Our sign-in rules were set up quickly and never revisited. Here's what we have today and a day of sign-in activity. I need to know which events worry you, and a better set of rules I can take to the IT director. Remember the front-desk staff at our clinics can't use their own phones.

Supporting Information: [Sign-in Log & Current Rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md)

<BR>

<table>
<tr>
<td>

**The Decision**

Case status: In progress.

</td>
</tr>
</table>

<BR>

## What's the Risk?

Sign-in rules set up quickly and never reviewed leave gaps an attacker can use: a trusted network that skips MFA, a protocol that cannot ask for it, and a session that stays open. Yesterday's log shows those gaps in use.

<BR>

## The Investigation

I reviewed [15 sign-in events against six existing rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md), using four questions to guide my investigation:

1. Which sign-in events need immediate investigation, and which are likely legitimate?
2. What should replace the current sign-in rules?
3. How can clinic staff use MFA on shared tablets without personal phones, and what is the trade-off?
4. How can we introduce the new policies without disrupting access?

<BR>

## What I Found

Five sign-ins to open, in this order.

| Severity | Account | Risk |
| --- | --- | --- |
| 🔴 Critical | breakglass-02 | Emergency admin, no MFA, no alert. |
| 🟠 High | s.park | Possible session theft. Austin, then Singapore nine minutes later. |
| 🟠 High | j.chen | Finance mailbox over IMAP. MFA was impossible. |
| 🟠 High | t.nguyen-admin | SMS on a personal laptop. The account is an admin. |
| 🟡 Medium | v.santos | Partner VPN treated as identity. No MFA. |

**Higher** means the log cannot explain it, and the account can do more damage. **Lower** means the likely user is visible, and the weakness is the control.

**Not incidents.** k.malik at HQ: trusted location, managed device. Clinic tablet: MFA timed out because staff cannot use personal phones.

[02. Event Triage](Documents/02.%20Event%20Triage.md)

<BR>

## Decisions & Recommendations

## Reflection & Next Steps

## Explore the Investigation
