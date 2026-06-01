# Anomalous Trading Detection Methodology

> Summarizes anomaly detection methods used in practice, including statistical models, machine learning approaches, and real-world cases.

## I. Detection Framework

Anomalous Trading Detection = **Feature Engineering** + **Detection Models** + **Disposition Policies**

### Pipeline

```
Raw Trade Stream → Feature Extraction → Real-Time Scoring → Rule Engine → Disposition Action
                        ↓
                   Offline Model Training (periodically updated)
                        ↓
                   Backtest Validation → Tune Parameters → Deploy
```

## II. Feature Engineering

### 2.1 Trade-Level Features

| Category | Specific Features | Source |
|----------|------------------|--------|
| Volume / Price | Single trade amount, cumulative amount, buy/sell direction | Order book |
| Frequency | Trade count per 1min / 5min / 1h | Sliding window counter |
| Price | Fill price deviation, bid-ask spread | Market data |
| Time | Trade interval, active hours | Timestamps |

### 2.2 Account-Level Features

| Category | Specific Features |
|----------|------------------|
| Behavioral | Login frequency, device switch count, IP change frequency |
| Asset | Balance change rate, deposit/withdrawal frequency, leverage utilization |
| Social | Linked account count, counterparty concentration |
| Historical | Prior violation count, alerts in the last 30 days |

### 2.3 Correlation Features

- **Device Fingerprint Clustering**: Account clusters sharing the same device
- **IP Segment Aggregation**: Accounts linked by same IP / C-class subnet
- **Fund Trail**: Deposit/withdrawal address relationship graph
- **Counterparty Network**: Frequent trading counterparty pairs

## III. Detection Models

### 3.1 Rule-Based Models

Applicable scenarios: known attack patterns, compliance requirements, rapid response

**Example Rules:**

```
Rule: Large Wash Trading Detection
  IF same IP segment AND buy/sell counterparties are each other
     AND fill price deviation < 0.1%
     AND trade count within 1h > 10
  THEN alert + manual review

Rule: Spoofing Detection
  IF order cancellation rate > 95%
     AND pre-cancellation order depth share > 20%
     AND repeated ≥ 3 times within 30min
  THEN restrict trading + review
```

### 3.2 Statistical Models

**Z-Score Anomaly Detection:**

```
Z = (X − μ) / σ

Applications:
- Trade frequency Z-score > 3 → anomalous high frequency
- Single trade amount Z-score > 4 → anomalous large amount
- Price deviation Z-score > 5 → anomalous price
```

**Sliding Window Statistics:**
- Short window (5min): Detect sudden spikes
- Medium window (1h): Detect sustained anomalies
- Long window (24h): Detect trend anomalies

**Interquartile Range (IQR) Method:**
```
IQR = Q3 − Q1
Lower outlier bound = Q1 − 1.5 × IQR
Upper outlier bound = Q3 + 1.5 × IQR
Extreme outlier = Q3 + 3 × IQR
```

### 3.3 Machine Learning Models

| Model | Applicable Scenario | Strengths | Weaknesses |
|-------|-------------------|-----------|------------|
| Isolation Forest | Unsupervised anomaly detection | No labels needed, fast | Poor interpretability |
| LOF (Local Outlier Factor) | Density-based anomalies | Good for local anomalies | High computational cost |
| AutoEncoder | High-dimensional features | Auto-learns features | Needs large normal dataset |
| XGBoost | Supervised classification | High accuracy, interpretable | Requires labeled data |

### 3.4 Graph Algorithms

**Application Scenarios:**

1. **Community Detection (Louvain Algorithm)**: Identify money laundering rings, wash trading clusters
2. **PageRank Variants**: Evaluate address importance / risk propagation in the network
3. **Shortest Path Analysis**: Fund path from flagged address to target address
4. **Subgraph Matching**: Identify known attack patterns (e.g., mixer usage patterns)

## IV. Real-Time Computation Architecture

```
Kafka (Trade event stream)
  → Flink (Window aggregation + feature computation)
    → Redis (Real-time feature store)
      → Scoring Service (Model inference)
        → Rule Engine (Rule matching)
          → Action (Pass / Alert / Block)
```

**Performance Requirements:**
- Event latency: P50 < 10ms, P99 < 50ms
- Throughput: > 100,000 events/sec
- Availability: 99.99%

## V. Model Evaluation

### 5.1 Offline Evaluation

| Metric | Description | Formula |
|--------|-------------|---------|
| Precision | Share of alerts that are truly anomalous | TP / (TP + FP) |
| Recall | Share of anomalies that are detected | TP / (TP + FN) |
| F1-Score | Harmonic mean of precision and recall | 2 × P × R / (P + R) |
| AUC | Model discrimination power | Area under ROC curve |

### 5.2 Online Evaluation

- **Alert Fatigue**: Daily alert volume, false positive rate trend
- **Rule Decay**: Change in rule hit rate over time (being circumvented)
- **Coverage Gaps**: Uncovered scenarios discovered via community feedback / security incident reviews

## VI. Representative Cases

### 6.1 Case: Correlated Account Wash Trading

**Discovery Process:**
1. A trading pair's volume suddenly surged 10× with price movement < 0.5%
2. Network analysis revealed 30+ accounts on the same IP segment with identical device fingerprints
3. Fund trail tracing: all accounts' funds ultimately swept to the same withdrawal address

**Disposition:**
- Freeze correlated account cluster
- Retroactively cleanse related trading volume
- Blacklist devices and IPs

### 6.2 Case: API Abuse

**Discovery Process:**
1. Monitoring detected sudden surge in calls for a specific API Key
2. Call pattern analysis: place order every 100ms, cancel, then re-place
3. Purpose: probe market maker quoting model via high-frequency probing

**Disposition:**
- API rate limit adjusted to 10 req/s
- Downgrade that API Key's privileges
- Add behavioral sequence anomaly detection rules

## VII. Summary

1. **No silver bullet**: No single model covers all anomalies; requires a combination of rules + statistics + ML + graph algorithms.
2. **Features > Models**: Good feature engineering matters more than tuning model parameters.
3. **Evaluation loop is essential**: Must have a backtesting framework to periodically validate model effectiveness.
4. **Business understanding**: Without understanding trading business logic, you cannot define what "anomalous" means.
5. **Cost balance**: Each additional detection layer = latency + false positive risk; requires trade-off analysis.
