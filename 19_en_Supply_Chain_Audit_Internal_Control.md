# Supply Chain Audit & Internal Control Practices

> Based on audit experience in large manufacturing enterprises (stainless steel / new energy supply chain). Summarizes the supply chain internal control framework.

## I. Audit Scope

Manufacturing supply chain spans the full chain from mine to finished product:

```
Mineral Procurement → Logistics & Transport → Warehouse Management → Production Consumption → Finished Goods Sales → Fund Recovery
       ↑                    ↑                      ↑                      ↑                      ↑                  ↑
  Procurement Audit    Logistics Audit      Inventory Audit         Cost Audit           Sales Audit        Treasury Audit
```

## II. Procurement Audit

### 2.1 Core Risks

| Risk Point | Manifestation | Audit Method |
|-----------|---------------|--------------|
| Bid Rigging | Suppliers taking turns winning bids | Bid IP / bid document comparison |
| Phantom Procurement | Procurement without actual delivery | Three-way match (contract + receipt + invoice) |
| Kickbacks | Procurement price significantly above market | Price benchmarking (same period / peer) |
| Supplier Monopoly | Overly high single-source share | Supplier concentration analysis |
| Credential Fraud | Supplier fabricating qualifications | Walkthrough testing + site visits |

### 2.2 Price Audit Methods

**Market Benchmarking:**
```
Price Deviation = (Procurement Price − Market Benchmark) / Market Benchmark
Red Alert: deviation > 5%
Yellow Alert: deviation > 3%
```

**Historical Trend:**
- 12-month price trend for the same item
- MoM / YoY anomalous fluctuation detection
- Seasonality pattern validation

### 2.3 Supplier Management Audit

- Is supplier onboarding process complete (qualification review, site visit, sample testing)?
- Is the approved supplier list updated periodically?
- Supplier performance evaluation (on-time delivery rate, quality pass rate, price competitiveness)
- Is the blacklist / elimination mechanism effectively enforced?
- Are related-party suppliers fully disclosed?

## III. Inventory Audit

### 3.1 Stocktaking Process

| Step | Content | Key Points |
|------|---------|------------|
| Pre-count | Plan, notify warehouse freeze | Surprise spot checks vs. scheduled counts |
| During count | Blind count (auditor records independently) | Do not cross-check with warehouse staff |
| Variance Analysis | Book vs. physical comparison | Variance > threshold → trace |
| Surplus / Shortage | Root cause analysis and accountability | Systemic vs. incidental |

### 3.2 Common Issues

- **Inflated Inventory**: Receipt recorded but goods not yet arrived
- **Quality Substitution**: QC grade inconsistent with actual
- **Slow-Moving Inventory**: No turnover for > N months without impairment provision
- **Off-Book Materials**: Consignment / custodial materials not recorded

### 3.3 Key Metrics

```
Inventory Turnover = COGS / Average Inventory
Aging Analysis: < 30 days / 30-90 days / 90-180 days / > 180 days
Slow-Moving Ratio = Slow-moving inventory / Total inventory
Shrinkage Ratio = Shortage value / Total inventory value
```

## IV. Logistics Audit

### 4.1 Freight Audit

| Method | Procedure | Tool |
|--------|-----------|------|
| Freight Benchmarking | Compare market freight rates for similar routes/distances | Logistics platform data |
| Ton-Kilometer Cost | Freight / (tonnage × distance) peer comparison | Industry reports |
| Empty-Run Check | GPS trajectory vs. actual waybill comparison | GPS data + waybills |
| Phantom Transport | Waybill vs. weighbridge slip vs. warehouse receipt match | Three-way match |

### 4.2 Bulk Commodity Logistics Specifics

- **Transit Loss Rate Control**: Loss standards for bulk shipments (nickel ore, coal, etc.)
- **Weight & Quality Inspection**: Third-party test comparison — loading port vs. discharge port
- **Demurrage**: Port demurrage accountability and cost control
- **Bonded Logistics**: Processing trade handbook reconciliation compliance

## V. Sales Audit

### 5.1 Credit Risk Control

```
Customer Credit Management Process:
  Qualification Review → Credit Limit Assessment → Payment Terms Approval → Dynamic Monitoring → Overdue Collection

Monitoring Metrics:
  - Accounts receivable turnover days
  - Overdue receivable ratio
  - Bad debt ratio
  - Top 5 customer concentration
```

### 5.2 Price Audit

- Sales price deviation from market price
- Arm's-length pricing for related-party transactions (transfer pricing risk)
- Discount / rebate approval authority compliance
- Long-term contract vs. spot price spread reasonableness

## VI. Cost Audit

### 6.1 Production Cost

| Element | Audit Focus | Method |
|---------|-------------|--------|
| Raw Material Cost | Is unit consumption reasonable? | Theoretical vs. actual unit consumption |
| Energy Cost | Abnormal power / gas consumption | Industry benchmark + historical trend |
| Labor Cost | Piece-rate wage reasonableness | Labor-hour quota vs. output matching |
| Manufacturing Overhead | Is allocation reasonable? | Cost driver analysis |

### 6.2 Cost Carry-Forward

- WIP vs. finished goods cost allocation
- By-product / scrap value accounting
- Reasonableness of cost method changes
- Adequacy of inventory impairment provisions

## VII. Internal Control Framework

### 7.1 Segregation of Duties

| Function | Roles That Must Be Separated |
|----------|------------------------------|
| Procurement | Requisition → Purchasing → Receiving → Payment |
| Sales | Pricing → Shipping → Invoicing → Collection |
| Warehouse | Custody → Bookkeeping → Stocktaking |
| Finance | Cashier → Bookkeeping → Review |

### 7.2 Approval Authority Matrix

```
Amount Tier        Procurement Approval    Sales Discount       Expense Reimbursement
< 10k              Dept. Manager           Dept. Manager        Dept. Manager
10k-100k           Divisional VP           Divisional VP        Finance Director
100k-1M            General Manager         General Manager      General Manager
> 1M               Board of Directors      Board of Directors   Board of Directors
```

### 7.3 Key Control Points (KCP)

- Procurement contract approval → Focus on supplier selection rationale
- Goods receipt → Focus on QC report and quantity verification
- Payment approval → Focus on three-way match
- Inventory count → Focus on book-physical variance handling
- Sales pricing → Focus on price deviation approval

## VIII. Digital Audit

### 8.1 Data Analysis Tools

- **SQL / Python**: Extract and analyze data from ERP (SAP / Oracle)
- **Power BI / Tableau**: Visualization dashboards
- **ACL / IDEA**: Professional audit analysis software
- **RPA**: Automate repetitive audit procedures (e.g., bank reconciliation)

### 8.2 Typical Analysis Scenarios

1. **Duplicate Payment Detection**: Same supplier, same amount, similar timing payment matching
2. **Anomalous Payment Detection**: Weekend/holiday payments, round-number large payments
3. **Ghost Employee Detection**: Payroll vs. attendance / access control data matching
4. **Split Procurement Detection**: Multiple small orders to the same supplier on the same day

## IX. Lessons Learned

1. **Auditing is not fault-finding; it's risk-finding** — Focus on high-risk areas, provide improvement recommendations to the business, not just point out errors.
2. **Data is more reliable than people** — If a system can surface the issue, don't rely on manual spot checks.
3. **Understand the business to audit it well** — If you don't know how nickel ore is priced or how stainless steel is made, you can't audit procurement or cost.
4. **Surprise stocktakes are the killer weapon** — The warehouse should never know when you're coming.
5. **Audit reports must drive action** — Issue + root cause + recommendation + remediation deadline + responsible person, forming a closed loop.
