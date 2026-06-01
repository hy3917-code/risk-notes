# Risk-Control-Side "Fund Reconciliation" Requirements Research (Personal Draft)

> Internal contact names and specific system codes removed.

## Background

Each business system has different objectives and risk tolerance, lacking a **unified funds security monitoring perspective**. Plan to build a reconciliation system **independent of business bookkeeping** for continuous verification and risk grading.

## Objectives

1. Monitor user fund anomalies
2. Monitor ledger-to-actual consistency
3. Provide basis for risk control decisions

## Three Core Questions

1. **Is the money correct?** — System ledgers vs. actual funds
2. **Is the discrepancy normal?** — Can business/accounting explain it?
3. **Is it dangerous?** — Should it be escalated? Should we intervene?

Fund flow (as I've diagrammed):

```
Onchain → Wallet Asset Ledger → Exchange User/Platform Ledger → Financial Ledger
```

## Research Targets and Key Points

### Wallet Team

- How does withdrawal approval determine "can withdraw"? Large/frequent thresholds?
- Wallet ledger vs. onchain mismatch: What duration is considered acceptable?
- Blind spots: sweeping delays, retry failures, miner fees, address allocation

### Exchange Team

- Do all balance-change scenarios have detailed records (rebates, deposits/withdrawals, trades, promotions, adjustments, etc.)?
- Risk points for shared funds across multiple business lines and matching/clearing delays?
- Any historical near-misses where "ledger balanced but funds unsafe"?

### Finance Team

- Signals that are normal from an accounting perspective but anomalous in real-time risk control?
- Interface methods with wallet/exchange teams? Are external withdrawals reviewed?
- 

## System Positioning (My Proposal)

- **Independent** from Wallet / Exchange / Finance
- Only performs: verification, monitoring, judgment — **does not participate in business bookkeeping**

```
System Data → Reconciliation Model → Discrepancy Identification → Risk Grading → Rules / Policies
```

## Rule Framework (Draft)

- Discrepancy amount, duration
- Large / high-frequency anomalies
- Cross-system inconsistencies

Output: alerts, restriction recommendations, event escalation.

## Expected Meeting Deliverables

1. Data inventory and sources
2. Unified understanding of discrepancy types
3. Phase 1 scope
4. Product / engineering roadmap

---

*Personal research outline. To be revised after review with each team.*
