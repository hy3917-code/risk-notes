# Risk Control Agent Technology — Study Notes

## 1. Agent vs. Chat

Agent = **Think → Try → Observe → Iterate** (ReAct).

Requires: model, tools, state/memory, control plane (observable / interruptible / auditable), structured output.

## 2. Tools

Enables the model to call APIs / DBs / files / business services.  
Practice: clear descriptions + input schemas; stable tool names; auth injected at runtime, never exposed to the model.

## 3. Control & Safety

- Limit call count / duration
- Manual confirmation for sensitive operations
- Retry / graceful degradation
- End-to-end audit trail

## 4. Memory & Context

Conversations must be recoverable; if too long, trim/summarize; store state as raw data, format only when needed.

## 5. Structured Output

Define schema first; on parse failure, retry / validate critical fields.

## 6. Graph (Multi-Step Workflow)

Nodes + explicit routing; interruptible and resumable; errors: retry / wait for human / surface exception.

## 7. Risk Control PoC Architecture (My Design)

- Stack: Spring Boot 3.x + Spring AI Alibaba + StateGraph
- **SupervisorAgent**: Plans steps, dispatches specialists, aggregates results
- Example specialists:
  - Asset Analysis (holdings, concentration)
  - Behavior Analysis (anomalous patterns)
  - Fund Analysis (deposits/withdrawals, fast in/out)
- Each specialist: ReactAgent + dedicated prompt + tool list + max iterations

## 8. My Personal Takeaways

Repetitive data lookups and summary writing in review operations are best suited for initial Agent deployment. For production: mock data → read-only tools → write operations with approval gates.

---

*External links (Anthropic, OpenLM, ModelScope, etc.) are in browser bookmarks; not repeated here.*
