# CEX Risk Control System Design & Practice

> Based on experience in centralized exchange risk control departments. Summarizes core modules, monitoring dimensions, and handling workflows.

## I. Risk Control Architecture Overview

CEX risk control is organized into four tiers:

| Tier | Responsibility | Latency Requirement |
|------|---------------|---------------------|
| **Real-Time Risk Control** | Transaction-link interception, anomalous order circuit breaking | < 50ms |
| **Near-Real-Time Monitoring** | Market anomalies, account behavior analysis | Seconds |
| **Offline Analysis** | Money laundering tracing, relationship network analysis | Hours / Days |
| **Post-Event Audit** | Compliance reporting, regulatory filings | Days / Weeks |

## II. Core Risk Control Scenarios

### 2.1 Market Manipulation Detection

**Detection Types:**

- **Wash Trading**: Frequent self-trading between accounts under common control to fabricate volume. Identified via device fingerprinting, IP correlation, and deposit/withdrawal path cross-validation.
- **Spoofing**: Large orders placed then rapidly canceled to mislead market price. Monitor accounts with cancellation rate > 95% and abnormally large order sizes.
- **Layering**: Multi-tiered orders creating false depth. Identified through order density and price distribution gradients.

**Core Metrics:**
- Self-trade ratio > threshold → alert
- Abnormal cancel/fill ratio
- Single-account depth share > N%
- Behavioral consistency within correlated account clusters

### 2.2 Anomalous Trading Monitoring

**Monitoring Dimensions:**

1. **Frequency**: Single-account TPS exceeding baseline by N standard deviations
2. **Amount**: Single / cumulative trade value hitting tiered thresholds
3. **Time**: Sudden high-frequency trading during inactive periods
4. **Price**: Fill price deviation from market price > threshold
5. **Counterparty**: Trading with flagged / high-risk addresses

**Circuit Breaker Mechanism:**
- L1 Alert: Manual review, no blocking
- L2 Alert: Restrict withdrawals, trading continues
- L3 Alert: Freeze account, suspend all operations

### 2.3 Deposit / Withdrawal Risk Control

| Scenario | Policy | Parameter |
|----------|--------|-----------|
| Large Withdrawal | Manual review + delayed settlement | > 50,000 USDT |
| New Device Withdrawal | 24h withdrawal limit | First ≤ 1,000 USDT |
| Risky Address | Block + report | Onchain blacklist hit |
| Frequency Anomaly | CAPTCHA + cooldown | 5 times / hour |
| Dispersed Outflows | Aggregate monitoring of linked accounts | Multiple addresses → same destination |

### 2.4 KYC / AML Compliance

- **Identity Verification**: Multi-factor (ID + facial recognition + liveness detection)
- **Sanctions Screening**: OFAC / UN / local regulatory lists
- **Transaction Monitoring**: Automated Suspicious Transaction Reporting (STR)
- **Travel Rule**: Cross-VASP transfer information transmission
- **Risk Assessment Model**: Behavior-based user risk tiering

## III. Technical Implementation Highlights

### 3.1 Rule Engine

```
Risk Rule = Trigger Condition + Execution Action + Cooldown Policy

Condition Layer:
  - Atomic Conditions: amount > X, frequency > Y, time ∈ [A, B]
  - Composite Conditions: AND / OR / NOT / SEQ (temporal sequence)
  - Statistical Conditions: sliding window mean / variance / Z-score

Action Layer:
  - Pass / Manual Review / Reject / Circuit Break / Report
```

### 3.2 Relationship Network Analysis

- **Graph Database** (Neo4j / TigerGraph): Store account-device-IP-address relationships
- **Community Detection Algorithms** (Louvain / Label Propagation): Identify syndicates
- **Risk Propagation**: N-degree neighbor risk scoring from flagged addresses

### 3.3 Real-Time Data Processing

- **Stream Processing Engine**: Flink / Kafka Streams
- **Time-Series Database**: InfluxDB / ClickHouse for metric storage
- **In-Memory Grid**: Redis Cluster for real-time counters and blacklist caching
- **Backtesting Framework**: Historical data replay to validate rule effectiveness

## IV. Metrics Framework

### Core Dashboard Metrics

| Metric | Description | Example Alert Threshold |
|--------|-------------|------------------------|
| Anomalous Trade Interception Rate | Blocked / Anomalous | Target > 99.5% |
| False Positive Rate | False blocks / Total blocks | < 0.1% |
| Rule Hit Rate | Share of trades hitting rules | Monitor trend |
| Review Latency | Average manual review duration | < 5 min |
| Risk Account Coverage | Flagged / Should-be-flagged | > 95% |

## V. Lessons Learned

1. **Don't over-stack rules**: Beginners tend to pile on rules, causing high false positive rates and heavy maintenance. Prioritize statistical models + a small set of core rules.
2. **Circuit breaking needs grayscale**: Never all-or-nothing. L1/L2/L3 tiered handling preserves both safety and user experience.
3. **Relationship networks are the killer weapon**: Single-account behavior may look normal, but within a relationship network you can uncover money-laundering rings and wash-trading clusters.
4. **Data and logs are the foundation**: The ceiling of risk control capability is determined by data quality. All operations must leave an audit trail.
5. **Communication cost with business teams**: Risk control is not purely technical — it requires continuous policy alignment with operations, compliance, and product.
