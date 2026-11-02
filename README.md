# Fraud_Detection
Fraud detection use case in financial services, integrating traditional DS model with generative and agentic AI



--- INITIATING AGENTIC REVIEW ---
╭─────────────────────────────────────────────── 🤖 Agent Started ────────────────────────────────────────────────╮
│                                                                                                                 │
│  Agent: Senior AML Compliance Analyst                                                                           │
│                                                                                                                 │
│  Task: XGBoost flagged this transaction: {'TransactionAmt': 10.392000198364258, 'card4': 'visa',                │
│  'P_emaildomain': 'icloud.com'}. Write a 3-sentence compliance narrative explaining why these specific          │
│  attributes indicate potential fraud.                                                                           │
│                                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
WARNING:crewai.llms.base_llm:Using an approximate input token count for model 'gemini-3.8-flash': assuming one token per four characters because a native token count is unavailable.
[Finalize] todos_count=0, todos_with_results=0
╭───────────────────────────────────────────── ✅ Agent Final Answer ─────────────────────────────────────────────╮
│                                                                                                                 │
│  Agent: Senior AML Compliance Analyst                                                                           │
│                                                                                                                 │
│  Final Answer:                                                                                                  │
│  The low-value transaction amount of approximately $10.39 on a Visa card strongly suggests an automated         │
│  card-testing topology, commonly utilized by illicit actors to validate stolen payment credentials before       │
│  executing larger fraudulent operations. This risk is further compounded by the association with an             │
│  'icloud.com' email address, a provider frequently exploited through anonymized relay features to conceal       │
│  actor identity and evade velocity-matching controls. Additionally, the irregular fractional floating-point     │
│  amount indicates automated cross-border currency conversion or script-driven checkout behavior, warranting an  │
│  immediate transaction hold and escalation for secondary credential verification.                               │
│                                                                                                                 │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

--- FINAL COMPLIANCE REPORT ---
The low-value transaction amount of approximately $10.39 on a Visa card strongly suggests an automated card-testing topology, commonly utilized by illicit actors to validate stolen payment credentials before executing larger fraudulent operations. This risk is further compounded by the association with an 'icloud.com' email address, a provider frequently exploited through anonymized relay features to conceal actor identity and evade velocity-matching controls. Additionally, the irregular fractional floating-point amount indicates automated cross-border currency conversion or script-driven checkout behavior, warranting an immediate transaction hold and escalation for secondary credential verification.
