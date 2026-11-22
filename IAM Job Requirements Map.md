# IAM Skills Map

**Northwind Health | Sign-in Triage & Policy Design**

This map links IAM Analyst job requirements to the work completed in this case study.

<BR>

| Job Requirement | Evidence in This Project |
| --- | --- |
| **Authentication and MFA** | [03. Proposed Sign-in Policies](Documents/03.%20Proposed%20Sign-in%20Policies.md): Proposed removing MFA bypasses at HQ and on the partner VPN, and requiring hardware keys for routine and emergency administrator sign-ins. |
| **IAM Troubleshooting** | [01. Sign-in Log & Current Rules](Documents/01.%20Sign-in%20Log%20%26%20Current%20Rules.md) · [02. Event Triage](Documents/02.%20Event%20Triage.md): Used the existing rules to explain why MFA was skipped at HQ and distinguished that from an MFA timeout on the shared clinic tablet. |
| **Access Risk Assessment and Investigation** | [02. Event Triage](Documents/02.%20Event%20Triage.md): Ranked five sign-ins by investigation priority and treated the Singapore patient portal sign-in as suspected session theft, not confirmed compromise. |
| **Access Control Design and Remediation Planning** | [03. Proposed Sign-in Policies](Documents/03.%20Proposed%20Sign-in%20Policies.md): Designed six replacement rules. Limited exceptions for older sign-in methods and set separate requirements for routine admin and emergency access. |
| **Testing and Verification Planning** | [03. Proposed Sign-in Policies](Documents/03.%20Proposed%20Sign-in%20Policies.md) · [04. Shared Tablet Sign-In](Documents/04.%20Shared%20Tablet%20Sign-In.md): Replayed all 15 events to estimate policy impact. Defined two handover checks: the previous session is closed and the next employee can sign in with their own account and key. |
| **Business Impact and Change Planning** | [04. Shared Tablet Sign-In](Documents/04.%20Shared%20Tablet%20Sign-In.md) · [05. Rollout Plan](Documents/05.%20Rollout%20Plan.md): Designed a sign-in method that does not require personal phones, explained the extra step at handover, and proposed a staged rollout with a pilot and rollback plan. |
| **Security Documentation and Communication** | [Project README](README.md): Summarised which events to investigate first, what to change and what the replay projected. Distinguished proposed outcomes from live results. |

<BR>

## 🔍 Areas of Interest

- **Microsoft Entra ID:** Validating sign-in policies and reviewing report-only outcomes in a lab.
- **PowerShell and Microsoft Graph:** Exporting and comparing sign-in records for repeatable investigations.

---

[Back to Project Overview](README.md)
