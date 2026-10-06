# Microsoft Entra ID Tenant Baseline

**Captured:** 6 October 2026
**Purpose:** Record the state of the lab tenant *before* any training lab changes it.
**Source:** Entra admin center exports (user list, licence list, Conditional Access policy JSON). Raw exports are stored in `private/` and are **not** committed - they contain object IDs and an email address.

> Nothing in this document has been changed. It is a snapshot only.

---

## 1. Licensing

| Item | Value |
|---|---|
| Licence | Microsoft Entra ID P2 |
| Purchased | 6 |
| Assigned | 5 |
| Available | 1 |
| Term ends | 20 August 2027 (set to cancel on expiration) |

### P2 holders

| Account | Department | Job title |
|---|---|---|
| Yetunde Duze | - | Global Administrator (tenant owner) |
| David Okafor | Executive | Chief Executive Officer |
| Wale Ibrahim | IT | Identity Administrator |
| Mei Chen | IT | Cloud Administrator |
| BreakGlass Admin | IT | Break-glass account |

---

## 2. Accounts

| Type | Count |
|---|---|
| Member accounts (lab personas, incl. tenant owner, break-glass and one risk-test account) | 29 |
| Guest accounts (external test account) | 1 |
| **Total** | **30** |

All member accounts are cloud-only (no on-premises sync).

---

## 3. Conditional Access policies

9 policies - **7 enabled, 2 report-only.** Created 13 Aug – 8 Sep 2026.

| Policy | State | Users in scope | Excluded | Apps | Condition | Grant |
|---|---|---|---|---|---|---|
| CA-01 Require MFA for Admin Portal Access | Report-only | All users | Break-glass | All apps | - | MFA |
| CA-02 Require MFA for Privileged Users | Enabled | Ama Mensah, David Okafor, Sofia Larsen | Break-glass | All apps | - | MFA |
| CA-03 Block Legacy Authentication | Enabled | All users | Break-glass, Yetunde Duze | All apps | Client apps: Exchange ActiveSync, Other | Block |
| CA-04 Require MFA for All Cloud Apps | Enabled | Ama Mensah, David Okafor, Mei Chen, Sofia Larsen, Wale Ibrahim | Break-glass | All apps | - | MFA |
| CA-05 Require MFA on Risky Sign-ins | Enabled | All users | Break-glass, Yetunde Duze | All apps | Sign-in risk: high, medium | MFA; sign-in frequency every time |
| CA-06 Require Entra Joined Device for IT Admins | Report-only | Mei Chen, Wale Ibrahim | Break-glass | All apps | - | `domainJoinedDevice` (as exported) |
| CA-07 Require Password Change on High User Risk | Enabled | Ama Mensah, David Okafor, Mei Chen, Sofia Larsen, Wale Ibrahim | Break-glass | All apps | User risk: high | MFA **and** risk remediation; sign-in frequency every time |
| CA-08 Executive High-Value Account Protection | Enabled | David Okafor, Sofia Larsen | - | All apps | Sign-in risk: low, medium, high | MFA |
| CA-09 Require Password Reset for High User Risk | Enabled | All users | Break-glass | All apps | User risk: high | Authentication strength (MFA) **and** password change |

---

## 4. Open questions - to be audited in Month 2 (IAM)

*Left blank on purpose. Fill in during the Month 2 identity audit.*

- 
- 
- 
