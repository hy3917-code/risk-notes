# Anti-Money Laundering & Customer Due Diligence SOP (Personal Notes)

> Abstracted from platform AML/CDD practices. Internal scoring interfaces and vendor names excluded.

## 1. Purpose

Standardize **CDD (Customer Due Diligence)** and **AML** processes: use address risk scoring to identify, assess, and handle high-risk behaviors, reducing money laundering, terrorist financing, and related risks.

## 2. Scope

- Covers registration, deposits, and withdrawals.
- Scoring dimensions (three sources, as I understand them):
  1. Address entity affiliation (mixers, sanctions, etc.)
  2. Historical transactions and interactions with known risky addresses
  3. Third-party malicious address databases (ransomware, theft, phishing, etc.)

## 3. Risk Levels (Reference)

| Level | Score | Meaning |
|-------|-------|---------|
| Severe | 91–100 | Directly linked to serious illegal activity |
| High | 71–90 | Fund flows with high-risk entities |
| Medium | 31–70 | Suspicious but unconfirmed |
| Low | 0–30 | No significant risk |

## 4. Registration EDD

High-risk users must provide supplementary materials: photo ID with selfie, proof of source of funds, etc. Reviewed within **48 hours**. If approved, marked for ongoing monitoring; if suspicious or documentation not submitted, deposit/withdrawal restricted.

## 5. Deposit Handling (My Common Judgment)

- Score **< 70**: Generally cleared.
- Score **≥ 70**: Branch based on amount and frequency:
  - First-time small amount (≤ 100 USD): Hold + prompt to verify source
  - Small amounts ≥ 3 times within 7 days: Hold + return
  - Large amount (≥ 1,000 USD) or address score ≥ 90 and amount ≥ 100 USD: Hold + request documentation, otherwise return

## 6. Withdrawal Handling

- **< 70**: Typically cleared.
- **≥ 70**: Large amounts / high-risk addresses require documentation; frequent small withdrawals may require switching addresses; even after approval, recommend switching to a low-risk address.

---

*Personal study notes. Specific thresholds subject to live production policies at the time.*
