# Commodity Hedging Risk Control Practices

> Based on experience in large manufacturing / commodity trading enterprises. Summarizes the risk management framework for hedging operations.

## I. Business Background

Large manufacturing enterprises (stainless steel / nickel / new energy materials) need to hedge raw material price fluctuation risks:

- **Buy-side Hedging**: Lock in future procurement costs (e.g., nickel, ferrochrome, coke)
- **Sell-side Hedging**: Lock in finished product sales prices (e.g., stainless steel, nickel sulfate)
- **Inventory Hedging**: Hedge against on-hand inventory devaluation risk

**Core Principle:** Hedging is for offsetting physical operational risks, not for speculative profit.

## II. Risk Identification

### 2.1 Market Risk

| Risk Type | Description | Example |
|-----------|-------------|---------|
| Price Risk | Severe futures price volatility | 2022 LME Nickel incident: price surged 250% in two days |
| Basis Risk | Abnormal spot-futures spread | Basis non-convergence in delivery month |
| Liquidity Risk | Unable to close positions in extreme markets | Limit-up / limit-down restrictions |
| FX Risk | Exchange loss on offshore hedging | LME USD-denominated vs. RMB costs |

### 2.2 Operational Risk

- **Margin Shortfall**: Extreme market margin call pressure (core lesson of the LME Nickel incident)
- **Over-hedging**: Futures positions exceeding physical exposure, essentially constituting speculation
- **Delivery Risk**: Insufficient deliverable supply or quality non-compliance
- **Counterparty Risk**: Improper handling by brokers / margin calls

### 2.3 Compliance Risk

- Hedge accounting (IAS 39 / IFRS 9) compliance requirements
- SASAC / CSRC regulations on state-owned enterprise hedging
- Cross-border capital flow forex controls

## III. Risk Control Framework

### 3.1 Organizational Structure

```
Board of Directors
  └─ Risk Control Committee
      ├─ Risk Control Department (independent from business units)
      │   ├─ Market Risk Group
      │   ├─ Credit Risk Group
      │   └─ Operational Risk Group
      ├─ Hedging Business Department
      └─ Finance Department (margin management)
```

### 3.2 Hedging Limit Management

| Dimension | Control Standard | Approval Level |
|-----------|-----------------|----------------|
| Total Hedging Scale | ≤ 100% of physical exposure | Risk Control Committee |
| Single-Instrument Cap | ≤ N% of total exposure | Risk Control Director |
| Monthly Open Volume | ≤ N% of monthly output | Business Head |
| Margin Utilization | ≤ N% of available funds | Finance Director |
| Stop-Loss Limit | Daily ≤ X / Cumulative ≤ Y | Trader |

### 3.3 Real-Time Monitoring Metrics

**Daily Monitoring Dashboard:**

```
□ Futures position vs. physical exposure matching degree
□ Margin utilization rate (current / warning / extreme)
□ Mark-to-market P&L (daily)
□ Basis trend (current vs. historical range)
□ Option Greeks (if using options for hedging)
□ Broker concentration (top 3 share)
□ Delivery-month positions (short squeeze risk?)
```

### 3.4 Stress Testing

**Scenario Design:**

| Scenario | Assumptions | Frequency |
|----------|-------------|-----------|
| Mild | Price movement ±10% | Weekly |
| Moderate | Price movement ±25% + basis widening | Monthly |
| Severe | Price movement ±50% + liquidity freeze | Quarterly |
| Extreme | Similar to 2022 LME Nickel event | Semi-annually |

**Test Outputs:**
- Margin call requirement
- Maximum loss amount
- Liquidity gap
- Whether contingency plan activation is needed

## IV. LME Nickel Incident Review & Lessons

### 4.1 Event Recap

March 2022: LME nickel futures surged from ~$30,000/ton to over $100,000/ton in two days. LME was forced to suspend trading and cancel billions in trades. Tsingshan Holding, as a major short, faced immense margin call pressure.

### 4.2 Core Lessons

1. **Excessive position concentration**: Overly large single-instrument, single-direction positions lacked resilience for extreme scenarios.
2. **Insufficient margin buffer**: Exchanges dramatically raised margin requirements in extreme markets (LME from 10% to 50%+), far exceeding normal projections.
3. **Underestimated liquidity risk**: Counterparties disappeared in extreme markets, making stop-loss impossible.
4. **Cross-market hedging risk**: Tsingshan shorted on LME but lacked physical delivery capacity (standard grade vs. non-standard).
5. **Opaque OTC positions**: Some positions were through OTC markets, making regulatory and risk oversight difficult.

### 4.3 Improvement Measures

- **Position diversification**: Multi-market, multi-instrument, multi-expiry distribution
- **Margin redundancy**: Reserve based on extreme (not normal) scenarios
- **Delivery capacity matching**: Ensure deliverable supply or lock in advance
- **OTC position transparency**: All derivative positions consolidated into risk control system
- **Contingency plans**: Pre-arrange extreme-market handling mechanisms with banks / brokers

## V. Hedge Accounting & Compliance

### 5.1 Hedge Relationship Documentation

Each hedge must document:
- Hedged item (physical asset / forecast transaction)
- Hedging instrument (futures / options / forwards)
- Hedge ratio
- Hedge effectiveness assessment method
- Treatment of ineffective hedge portion

### 5.2 Hedge Effectiveness Assessment

**Regression Method:**
```
Δ Spot Price = α + β × Δ Futures Price + ε

Hedge Effectiveness Conditions:
- R² > 80%
- 0.8 < β < 1.25
```

**Dollar Offset Method:**
```
Hedge Effectiveness = Δ Fair Value of Hedging Instrument / Δ Fair Value of Hedged Item
Effective Range: 80% – 125%
```

## VI. Lessons Learned

1. **The essence of hedging is risk management, not a profit center** — Risk control must be independent from business; decision-making authority and oversight must be separated.
2. **Extreme scenarios must be taken seriously** — It's not about whether they'll happen, but whether you can survive when they do.
3. **Margin is the lifeline** — Margin call requirements can grow exponentially in extreme markets.
4. **Delivery capacity equals bargaining power** — In the LME incident, having or not having physical supply was the difference between life and death.
5. **Penetrating risk control** — All derivative positions (including OTC) must be measured and monitored uniformly, with no blind spots.
