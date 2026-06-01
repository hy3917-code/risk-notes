# Automated Alert War Room Demo Notes (OpenClaw + MCP)

> Sanitized version of the presentation deck; excludes API keys and internal repo paths.

## Pain Point

Alerts → Manual investigation of orders / trades / transfers → Write reports → Propose actions. **MTTD/MTTR is long**; alerts become noise.

## Goal

```
Alert → AI Agent Automated Investigation → Report + Action Recommendations → Human Review & One-Click Execution
```

## What Is OpenClaw (My Understanding)

An open-source personal AI assistant framework: connects to LLMs + MCP tools + multi-channel; runs locally.

**Why MCP**: Interface with external systems like order/trade services; write once, use across multiple clients; process isolation.

**When to use AgentSkills**: Local files, browser automation, rapidly creating new capabilities.

## Demo Architecture

```
User → LLM → Risk Investigation Tools (MCP) → Report
```

6 tool examples: `getOrders` / `getTrades` / `getTransfers` / `getProfile` / `calculateRiskScore` / `applyAction`

## Running (Reference)

- Node 22+
- `npm install` → Set `DASHSCOPE_API_KEY` (or swap model env) → `npx tsx src/cli.ts`
- Lightweight CLI; full OpenClaw installation not required

## Demo Scenario (Fictional Accounts)

- Perpetual-spot spread arbitrage + API high-frequency order cancellation
- ACC001: High risk (spread ~8%, high hedge ratio, fast in/out, new account, VPN)
- ACC002: Low risk comparison

## Scoring

Composite 0–100: Low 0–39 / Medium 40–69 / High 70–100, four dimensions + evidence + recommended action.

## Demo Boundaries (I Will Disclose)

- ✅ Workflow, explainable scoring, Chinese-language interaction
- ❌ Pre-set mock data, actions are log-only, not connected to live trading

---

*PoC study notes. Not a production solution.*
