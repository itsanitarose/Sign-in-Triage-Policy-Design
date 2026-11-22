# Sign-in Triage & Policy Design

**IAM skills demonstrated:** Sign-in log analysis, risk triage, MFA policy design, and rollout planning.

## 🎫The Ticket

It's 16 November 2026, my **7th week** at Northwind Health.&#x20;

My manager writes:


> Our sign-in rules were set up quickly and never revisited. Here's what we have today and a day of sign-in activity. I need to know which events worry you, and a better set of rules I can take to the IT director. Remember the front-desk staff at our clinics can't use their own phones.

<BR>

Supporting Information: [Sign-in Log & Current Rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md)

<BR>

<table>
<tr>
<td>

**Case at a Glance**

Investigate `breakglass-02` first, then `s.park`. The first reached the admin console with no MFA and no alert. The second reached the patient portal from Singapore nine minutes after Austin.<BR><BR>
Remove MFA bypasses at HQ and on the partner VPN. Block older sign-in methods, with temporary exceptions for the scanner and old mail app. Require a hardware key and a compliant device for routine admin access. Alert on every emergency account sign-in. At the front desk, keep the tablet shared and give each staff member their own account and hardware key. No personal phone needed.<BR><BR>
Turn the rules on in stages. Preview in report-only, pilot with IT, one vendor group and Clinic 12, and roll back any rule that stops essential work. Retire the shared account only after Clinic 12 passes the handover check.<BR><BR>
**Projected impact:** 9 of 15 sign-ins would have been blocked or challenged. #15 stays an investigation. The 12-hour rule would not have stopped it.

</td>
</tr>
</table>
<BR><BR>

## The Investigation in Detail:


<BR>

## What's the Risk?


Sign-in rules set up quickly and never reviewed can leave security gaps, weak default settings, or outdated login methods that attackers could exploit. The risk is unauthorised access to sensitive information or administrator accounts.

Shared clinic tablets introduce another risk. If staff use the same account or inherit another person's session, it becomes difficult to know who accessed patient information or performed an action. This puts both patient privacy and individual accountability at risk.

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

- **Close sign-in gaps.** Remove MFA bypasses at HQ and on the partner VPN. Block older sign-in methods that cannot support MFA, with temporary exceptions for the scanner and old mail app. Require a hardware key and a compliant device for routine admin access, and alert on every successful emergency account sign-in. [Proposed sign-in policies](Documents/03.%20Proposed%20Sign-in%20Policies.md)
- **Protect each tablet handover.** End the outgoing employee’s portal session before the next employee signs in with their own account and hardware key. No personal phone is needed. Retire the shared account only after Clinic 12 passes its access and handover checks. [Shared tablet sign-in](Documents/04.%20Shared%20Tablet%20Sign-In.md)
- **Roll out in stages.** Review the rules in report-only mode, then pilot them with IT, one vendor group and Clinic 12. Roll back any rule that disrupts essential access. [Rollout plan](Documents/05.%20Rollout%20Plan.md)

**Projected impact:** The proposed rules would have blocked or challenged 9 of the 15 recorded sign-ins. Three of those blocks depend on retiring the shared clinic account. I replayed the supplied log; I did not test the rules in a live tenant.

<BR>


## Reflection & Next Steps

This investigation reminded me why sign-in activity needs careful judgement. What looks suspicious is not always a compromised account, and a successful sign-in does not necessarily mean access was secure.

The clinic exemption restored access, but staff still used a shared account. Before retiring it, I would test that the next employee sees a sign-in prompt rather than the previous employee’s patient data, then confirm they can sign in with their own account and hardware key without a personal phone.

The hardest call was #15. For the replay, I treated the 18:09 Singapore event as a continuation of the session that began in Austin at 18:00. On that assumption, only nine minutes had passed, so my proposed 12-hour rule would not have required reauthentication. The patient portal could address that gap by pausing access when it detects a change in network location and sending the user to Entra to reauthenticate. That portal control was outside the scope of my Entra-only redesign. I kept #15 as an investigation priority and did not count it as a challenge in the replay.

<BR>


## Explore the Investigation

| Document | Focus |
| --- | --- |
| [01. Sign-in Log & Current Rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md) | The 15 recorded sign-ins and the six rules in place at the time. |
| [02. Event Triage](Documents/02.%20Event%20Triage.md) | The five sign-ins I’d investigate first and two that were likely legitimate. |
| [03. Proposed Sign-in Policies](Documents/03.%20Proposed%20Sign-in%20Policies.md) | Six replacement rules and a replay of all 15 sign-ins. |
| [04. Shared Tablet Sign-In](Documents/04.%20Shared%20Tablet%20Sign-In.md) | How clinic staff sign in without personal phones and what changes at handover. |
| [05. Rollout Plan](Documents/05.%20Rollout%20Plan.md) | How to preview, pilot and expand the rules, and when to roll them back. |

---
[← Week 6: RBAC Role Redesign](https://github.com/itsanitarose/RBAC-Role-Redesign) · [All Case Studies](https://github.com/itsanitarose/IAM-Case-Studies)
