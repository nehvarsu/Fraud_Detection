# Agentic-Fraud-Detection-XGBoost-LLM
Fraud detection use case in financial services, integrating traditional DS model with generative and agentic AI

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

While having a dedicated agent for each fraud type sounds intuitive, structuring agents by Data Domain (Cyber vs. Finance) rather than Typology (ATO vs. Carding) is the enterprise standard for three specific reasons:

Token Efficiency and Compute Cost: If you build an ATO Agent, a Carding Agent, and a Cross-Border Agent, we do not know which typology applies to a new transaction yet. We would have to trigger all of them in parallel on every single alert just to see which one "claims" the fraud. That drastically multiplies our API costs, token usage, and latency.

Organizational Mirroring: Multi-agent swarms work best when they mimic real-world human operations. We have an InfoSec team that analyzes devices ( Cyber Agent) and an AML team that looks at transaction velocity (Financial Agent). The Director Agent mirrors the actual human Risk Manager who reads both objective reports and makes the final classification.

Preventing Hallucinations: If we feed an "ATO Agent" a transaction that is actually just Cross-Border fraud, the agent's prompt is heavily biased toward finding ATOs. This can cause the LLM to hallucinate account takeover signals just to fulfill its specific role. Domain agents stay mathematically objective (e.g., "The device is an iPhone, the IP is domestic").

In a real-world sprint, we ship the Domain-to-Director pipeline first to prove value and baseline the latency, and then introduce a routing layer only when compute costs force our hand.

# Agentic AI for Fraud Triage: A Hybrid ML Architecture

This repository demonstrates an enterprise-grade fraud detection pipeline that bridges traditional high-speed machine learning with modern generative AI. 

A critical bottleneck in financial crime operations is translating statistical risk scores into actionable, human-readable compliance narratives. This architecture solves that by using a lightweight XGBoost model for real-time anomaly detection, followed by an asynchronous Multi-Agent Swarm to autonomously investigate and generate Suspicious Activity Reports (SAR).

## 🧠 System Architecture

1. **Typology Engineering (EDA):** Reverse-engineered the binary `isFraud` flag from the IEEE-CIS dataset into distinct business typologies (Account Takeover, Velocity Carding, Cross-Border). Profiling proved that different typologies exhibit entirely different behavioral signatures, requiring specialized investigation logic.
2. **The Speed Layer (XGBoost):** Ingests transaction telemetry to generate rapid baseline probability scores. Tree-based models effectively handle the extreme right-skew of financial velocity metrics without massive standardization overhead.
3. **Semantic Vectorization (LangChain & Google GenAI):** Transforms high-cardinality categorical data (e.g., anonymized device IDs, burner email domains) into unstructured text memos, vectorized via `text-embedding-004` to capture semantic risk relationships that cause traditional models to overfit.
4. **Agentic Explainability (CrewAI & Gemini 3.8-Flash):** An autonomous task force investigates flagged transactions out-of-band:
   * **Cyber Intelligence Agent:** Analyzes the digital footprint (devices, IPs, emails) for spoofing and ATO signals.
   * **Financial Forensic Agent:** Evaluates transaction velocity, card networks, and amount anomalies.
   * **Director of Fraud Operations:** Synthesizes the domain reports to classify the exact typology and generate a final 3-sentence Suspicious Activity Report (SAR) for human investigators.

## 🛠️ Technical Stack
* **Traditional ML:** XGBoost, Scikit-Learn, Pandas, Seaborn
* **Agentic Frameworks:** CrewAI, LangChain
* **LLM & Inference:** Google Gemini API (3.8-Flash & Embeddings)
* **Design Patterns:** Domain-to-Director Multi-Agent Routing, Heuristic Clustering

## 🚀 Key Features
* **Zero-Cost Cloud Implementation:** Built entirely on Kaggle datasets and the Gemini API Free Tier.
* **Resilient API Guardrails:** Includes automated rate-limit handling (15 RPM compliance) and asynchronous execution (`kickoff_async()`) to bypass Colab event loop collisions.
* **Secure Execution:** Architecture relies entirely on native secret managers, ensuring zero API key leakage.
