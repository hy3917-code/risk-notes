# Onchain Asset Risk Control Practices

> Based on risk control experience from STO / onchain asset issuance projects. Summarizes core practices: smart contract security, oracle attack defense, cross-chain bridge monitoring.

## I. Onchain Risk Control vs. CEX Risk Control

| Dimension | CEX Risk Control | Onchain Risk Control |
|-----------|-----------------|---------------------|
| Control Method | Centralized interception | Onchain contracts + offchain monitoring |
| Latency Requirement | Milliseconds | Block-level (seconds ~ minutes) |
| Reversibility | Can be rolled back | Irreversible (requires governance multi-sig) |
| Anonymity | KYC-bound | Address-anonymous |
| Attack Surface | Account / trade layer | Contract vulnerabilities / oracles / MEV |

## II. Smart Contract Risk Control

### 2.1 Pre-Deployment Security Checklist

```
Checklist:
□ Reentrancy attack protection (CEI pattern / ReentrancyGuard)
□ Integer overflow (Solidity 0.8+ built-in / SafeMath)
□ Access control (Ownable / RBAC)
□ Flash loan attack (trustworthiness of price oracle sources)
□ Front-running protection
□ Timestamp dependency (block.timestamp risks)
□ Random number security (do not use onchain data as randomness source)
□ Governance attack (proposal-execution timelock)
□ Upgrade security (proxy pattern / multi-sig control)
```

### 2.2 Runtime Monitoring

**Monitoring Dimensions:**

1. **Large Transfers**: Single tx > X% of total supply → alert
2. **Owner Operations**: Ownership transfer / pause / upgrade → real-time notification
3. **Abnormal Calls**: Unpublished functions being called / high-frequency failed transactions
4. **Fund Flows**: Abnormal contract balance changes / unusual withdrawals
5. **Gas Anomalies**: Transaction gas far exceeding normal → possible MEV attack

**Toolchain:**
- Tenderly / OpenZeppelin Defender: Real-time alerts
- Forta Network: Decentralized monitoring network
- The Graph: Onchain data indexing and querying

### 2.3 Case Study: Flash Loan Attack Defense

**Attack Pattern:**
1. Attacker borrows large assets in a single transaction (flash loan)
2. Exploits contract logic flaws to manipulate prices
3. Arbitrages and repays the loan; the contract bears the loss

**Defense Measures:**
- Use TWAP (Time-Weighted Average Price) instead of instantaneous price for oracles
- Set minimum delay (timelock) for critical operations
- Set per-transaction slippage caps
- Integrate decentralized oracles such as Chainlink / Pyth

## III. Oracle Security

### 3.1 Risk Types

| Risk | Description | Example |
|------|-------------|---------|
| Price Manipulation | Distorting spot price via large DEX trades | Flash loan + price manipulation |
| Data Latency | Offchain price updates lagging | During extreme market volatility |
| Single Point of Failure | Reliance on a single oracle node | Node outage |
| Sybil Attack | Forging multiple nodes to report false data | Low-cap tokens |

### 3.2 Defense Architecture

```
Price Feed Pipeline:
  Multi-source (CEX + DEX aggregation)
    → Median aggregation
    → Outlier removal (deviation from median > N%)
    → TWAP smoothing
    → Freshness check (data staleness)
    → Onchain consumption
```

## IV. Cross-Chain Bridge Risk Control

### 4.1 Core Risks

- **Validator Attack**: Controlling multi-sig validators → forge withdrawal proofs
- **Message Replay**: Same cross-chain message executed multiple times
- **Liquidity Drain**: Massive single-side asset withdrawals
- **Contract Upgrade Risk**: Upgrade introducing vulnerabilities

### 4.2 Monitoring Strategies

| Monitor Item | Method | Response |
|-------------|--------|----------|
| Large Cross-Chain Transfer | TVL share > N% | Delayed processing + manual confirmation |
| Validator Anomaly | Signature set changes | Pause bridge + notify |
| Liquidity Monitoring | Asset balances per chain | < threshold → pause withdrawals |
| Message Queue Backlog | Pending message count | Scale or degrade |

## V. Onchain Data Analytics

### 5.1 Common Tools

- **Dune Analytics**: SQL query onchain data, build dashboards
- **Nansen**: Labeled addresses, smart money tracking
- **Chainalysis / TRM Labs**: Compliance-grade onchain analysis
- **Etherscan API**: Basic transaction queries and contract verification

### 5.2 Key Analysis Scenarios

1. **Token Holder Concentration**: Top 10 address holding share
2. **Linked Address Discovery**: Fund flow graph analysis
3. **Price Anomaly Detection**: DEX price vs. CEX price spread
4. **Contract Interaction Heatmap**: Identify high-frequency / abnormal interaction patterns
5. **MEV Extraction Analysis**: Sandwich / arbitrage behavior identification

## VI. Practical Experience

1. **The core of onchain risk control is "monitoring + response"**: Unlike CEX, you can't intercept in real time, so early detection + fast multi-sig response is critical.
2. **Oracles are the Achilles' heel**: 90% of DeFi attacks involve price manipulation. TWAP + multi-source aggregation is the minimum configuration.
3. **Toolchain matters more than code**: Forta alerts + Tenderly simulation + Dune analytics form the complete pipeline.
4. **Governance security cannot be ignored**: Multi-sig key management, timelock parameters, proposal thresholds all directly determine protocol security.
5. **Cross-chain security is the next frontier**: 2022–2024 cross-chain bridge theft exceeded $2 billion. Bridge risk control should be no less rigorous than the chain itself.
