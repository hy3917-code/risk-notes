# Playwright CLI + Claude: Low-Token Automated Testing (Personal Summary)

## Concept

Browser automation (Playwright) handles the "hands and feet," while AI only acts as the "brain" when needed — understanding tasks, breaking down steps, orchestrating Skills. **Token usage should ideally approach zero.**

## Four-Layer Architecture

| Layer | Content |
|-------|---------|
| Preparation | Node.js, Playwright, Chrome |
| Capability (Skill) | Open requirements, learn business logic, generate test cases, verify against cases, produce reports |
| Task | Multiple Skills chained into a complete workflow |
| AI (Optional) | Task understanding, decomposition, generating invocation chains |

```
AI Understanding → Execution Flow → Invoke Skills → Playwright → Results
```

## Three Principles

1. **Avoid AI when possible** — More stable, cheaper
2. **Skill-ify** — `login()`, `search()`, etc., reusable and composable
3. **CLI-first** — Controllable, reproducible, easy to debug

## A Case I've Done

- Requirement: Add export functionality to "Withdrawal Review" in the Review Center
- Steps: Read requirements → Generate test cases → Verify in **test environment risk control console** → Aggregate results
- Pending: Automated CAPTCHA input

## Positioning

Not "pure AI automation," but **automation + AI augmentation**.

---

*Internal requirement links removed; environment addresses described generically as test console.*
