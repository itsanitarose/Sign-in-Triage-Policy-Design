
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

In a clinic, shared tablets introduce another concern: knowing who is actually signed in. If staff share accounts or inherit someone else’s session, patient information can be accessed without a reliable record of who accessed it.
<BR>

## The Investigation

I reviewed [15 sign-in events against six existing rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md), using four questions to guide my investigation:

1. Which sign-in events need immediate investigation, and which are likely legitimate?
2. What should replace the current sign-in rules?
3. How can clinic staff use MFA on shared tablets without personal phones, and what is the trade-off?
4. How can we introduce the new policies without disrupting access?

<BR>

## What I Found

Of the 15 sign-ins I reviewed, these are the five I’d investigate first, in priority order.

| Investigation priority | Event | Account&nbsp;identifier | Why I’d investigate |
| --- | --- | --- | --- |
| **P1** | #1 | `breakglass-02` | Treat as suspected unauthorised emergency access: an unmanaged device reached the admin console without an MFA prompt or alert, exposing privileged access without notifying the team. |
| **P2** | #15 | `s.park` | Investigate as suspected session theft: a Singapore sign-in with unknown device status used an existing session to reach the patient portal nine minutes after Austin, putting patient data at risk. |
| **P3** | #5 | `j.chen` | Investigate as suspected mailbox exposure: two successful IMAP sign-ins from Romania (#5 and #6) reached the finance mailbox through a flow that could not prompt for MFA. |
| **P4** | #12 | `t.nguyen-admin` | Investigate as a privileged access risk: an unmanaged personal laptop reached the admin console using SMS MFA, so stolen credentials and a phished code could give an attacker console access. |
| **P5** | #7 | `v.santos` | Investigate as a vendor access risk: the trusted partner VPN let a guest on an unmanaged device reach the billing app without an MFA prompt, leaving billing access exposed if the guest’s credentials were stolen. |

I ranked the sign-ins by potential impact, unusual activity, and weaknesses in sign-in controls.

[02. Event Triage](Documents/02.%20Event%20Triage.md)

<BR>

## Decisions & Recommendations

## Reflection & Next Steps

## Explore the Investigation
