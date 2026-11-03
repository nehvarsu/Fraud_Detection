# Agentic-Fraud-Detection-XGBoost-LLM
Fraud detection use case in financial services, integrating traditional DS model with generative and agentic AI

Final Agentic Output:


<img width="1477" height="662" alt="image" src="https://github.com/user-attachments/assets/0213e50a-90df-493e-8218-57fea89a8209" />

# Agentic AI Fraud Detection Pipeline

A hybrid machine learning architecture that bridges traditional high-speed tabular scoring with modern generative AI for automated compliance triage. 

This project tackles a major bottleneck in financial crime operations: translating statistical risk scores into actionable, human-readable compliance narratives for investigation teams.

## Architecture
1. **The Core Classifier (XGBoost):** Ingests the IEEE-CIS Fraud Detection dataset (memory-optimized) to generate rapid baseline probability scores for fraudulent transactions.
2. **Contextual Embeddings (LangChain & Gemini API):** Transforms raw categorical data (card types, email domains) into unstructured text memos, which are vectorized using Google's `text-embedding-004` (via dynamic API discovery) to capture semantic relationships.
3. **Agentic Explainability (CrewAI):** An autonomous `Senior AML Compliance Analyst` AI agent evaluates flagged transactions. It acts as an asynchronous investigator, translating the numerical anomaly into a 3-sentence, human-readable compliance report.

## Technical Stack
* **Modeling:** XGBoost, Scikit-Learn, Pandas
* **AI/LLM Frameworks:** CrewAI, LangChain
* **Embeddings & Inference:** Google Gemini API (Gemini 3.8-Flash)
* **Environment:** Python, Google Colab

## Key Features
* **Zero-Cost Cloud Implementation:** Built entirely on Kaggle datasets and the Gemini API Free Tier.
* **Resilient API Guardrails:** Includes custom circuit breakers, automated rate-limit handling (15 RPM compliance), and dynamic model discovery to bypass SDK namespace collisions.
* **Safe Secrets Management:** Architecture relies on Colab's native Secrets manager, ensuring zero API key leakage in the public repository.

Multi-Agent Swarm: a specialized team of AI agents
Phase 1: The "Agent-Informed" EDA:

By plotting the transaction amounts on a log scale, I proved that a rigid, rules-based threshold for fraud detection is insufficient. A $150 transaction might be completely standard for one user, but it sits dead-center at the median for an Account Takeover. This variance in financial distribution is exactly why I moved beyond a single XGBoost score and architected an Agentic AI system. I needed a specialized Financial Agent that could evaluate the dollar amount dynamically in the context of the specific typology, rather than relying on a static numerical cut-off.

<img width="872" height="482" alt="image" src="https://github.com/user-attachments/assets/40a9a5aa-475b-4a11-9f9e-5e29cbd72766" />


