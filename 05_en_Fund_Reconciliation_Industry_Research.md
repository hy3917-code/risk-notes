# Fund Reconciliation — Industry Research Notes (Personal Edition)

## I. Reconciliation Flow (Onchain + Accounting)

1. **Onchain Verification**: Scan TXIDs by currency/address via blockchain explorers to prevent "empty deposits."
2. **Accounting Ledger**: Onchain records vs. user ledger — "Inflows − Outflows = Balance Change."
3. **Hot/Cold Wallet Transfers**: Gas fees, sweeping, and fund allocation must be traceable.

## II. Exchange Types (My Comparison Table)

| Type | Representative | Characteristics |
|------|---------------|-----------------|
| Large Composite Exchange | Tier-1 comprehensive | Standalone risk-grade reconciliation; dual-run for existing + incremental data; heavy legacy, high anomaly volume |
| Compliance / Fiat-Friendly | US-listed exchanges, etc. | General ledger matches onchain; audit-friendly; often T+1, weak real-time |
| Heavy Derivatives | Top derivatives exchanges | High incremental event sensitivity, position-level; often siloed from financial view |
| Small / Mid-size | New exchanges | Short link chain, easy to modify; single-point risk large without independent risk reconciliation |

## III. Real-Time vs. Scheduled

**Wallet Reconciliation**: Hot/cold wallets, onchain, custodians — balances, deposit/withdrawal TXs, sweeping, gas, freezes → **Asset authenticity**

**Exchange Reconciliation**: Matching engine vs. external venues — orders, fills, positions, freezes, P&L → **Business authenticity**

**Financial Reconciliation**: Wallets + third-party payments + general ledger → **Accounting compliance**

## IV. The Three Layers Cannot Substitute for Each Other

- Trades matching ≠ Money matching
- Money matching ≠ Wallet actually has funds
- Wallet having funds ≠ Accounting is sound

**Recommended sequence**: Exchange (near-real-time) → Wallet (authenticity) → Financial (result validation)

## V. Research Summary (Major Platform Practices)

Common reconciliation design: **Define business model → Abstract reconciliation model → Select approach → System design**

Exchange PoR / Reserve Proof modules (Binance, OKX, bitFlyer, BingX, etc.) — My key takeaways: "liability snapshot + onchain assets + coverage ratio." Details in public PoR reports; internal methodologies not included.

---

*Public information + personal summary. Not a company deliverable.*
