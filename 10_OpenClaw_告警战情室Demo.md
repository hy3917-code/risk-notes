# 告警自动战情室 Demo 笔记（OpenClaw + MCP）

> 分享稿脱敏版；不含 API Key、内部仓库路径。

## 痛点

告警 → 人工查订单/成交/转账 → 写报告 → 提处置，**MTTD/MTTR 长**，告警变噪音。

## 目标

```
告警 → AI Agent 自动调查 → 报告 + 处置建议 → 人审核一键执行
```

## OpenClaw 是什么（我理解的）

开源个人 AI 助手框架：接大模型 + MCP 工具 + 多通道；可本地跑。

**为什么用 MCP**：对接订单/成交等外部系统；写一次多客户端可用；进程隔离。

**什么时候用 AgentSkills**：本地文件、浏览器自动化、临时写新能力。

## 本 Demo 架构

```
用户 → 大模型 → 风控调查工具(MCP) → 报告
```

6 个工具示例：`getOrders` / `getTrades` / `getTransfers` / `getProfile` / `calculateRiskScore` / `applyAction`

## 运行（备忘）

- Node 22+  
- `npm install` → 设置 `DASHSCOPE_API_KEY`（或换模型 env）→ `npx tsx src/cli.ts`  
- 轻量 CLI 可不装完整 OpenClaw  

## 演示场景（虚构账户）

- 永续-现货价差套利 + API 高频撤单  
- ACC001：高风险（价差 ~8%、对冲率高、快进快出、新户 VPN）  
- ACC002：低风险对比  

## 评分

综合 0–100：低 0–39 / 中 40–69 / 高 70–100，四维度 + 证据 + 建议动作。

## Demo 边界（我自己会说明的）

- ✅ 流程、可解释评分、中文交互  
- ❌ 预设 mock 数据、处置仅日志、未接真实交易  

---

*PoC 学习笔记，非生产方案。*
