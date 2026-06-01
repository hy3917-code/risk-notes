# New Risk Control System — Current State (Personal Understanding)

> Internal product names (e.g., fiat channel brands) removed; described using generic module names.

## I. Functional Architecture

Pipeline: **Rule Configuration → Real-Time Decisioning → Manual Review → Monitoring & Alerting → Data Backtesting**

```
Business Request → Real-Time Engine / Monitoring Engine → Review Center / Alerts
                        ↑
               Metrics System (Data Sources, Dimensions, Metrics, Engine Logs)
```

### 1. Review Center

Unified management of multi-business review tasks, for example:

- Onchain Withdrawals: currency, tx hash, address, quantity, fee, hit rules
- Fiat / Payment Channel Outflows: channel, payee info, exchange rate, order ID
- Onchain Deposit Reconciliation
- Marketing Campaign Eligibility

### 2. Risk Tags

- Custom Tags: name, level, description, operator
- Entity Binding: user IDs, etc.; records reason, repeat count, last-tagged time

### 3. Decision Engine

- Scenarios: segmented by business line; grayscale rollout, owner, enable/disable
- Parameters: thresholds, toggles
- Variable Library: scenario variables, constants, derived metrics

### 4. Monitoring Engine

- Monitor Events: business events, bypass ratio, fallback policies
- Monitor Rules: scripted logic (e.g., Groovy); supports rule hits, alerts, policy results

### 5. Metrics System

Data source ingestion, dimensions, metric configuration, backtesting, engine log query.

## II. Evolution Directions I'm Watching (Agent)

| Scenario | Input | Output | Value |
|----------|-------|--------|-------|
| Review Assistance | Cases + Tags + Relationship Graph | Recommendations + Summaries | Reduce manual review time |
| Policy Tuning | Block rate, false positive rate, pass rate | Parameter suggestions + A/B | Adaptive thresholds |
| Alert Noise Reduction | High-frequency alert logs | Aggregation + Suppression Rules | Reduce operational fatigue |

## III. Personal Summary

The system already covers the main chain of policy → review → tags → monitoring, making it suitable as a foundation for subsequent Agent pilots. My next priority is to implement two PoCs: "Review Assistance" and "Alert Noise Reduction."

---

*Compiled May 2026*
