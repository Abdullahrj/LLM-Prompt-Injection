# AI-Red-Teaming
Brief Proof of Concept on a working LLM Prompt Injection
Target System
Public Large Language Model used as a conversational assistant (DeepSeek Chat), representative of customer-facing LLM deployments.
________________________________________
1. Objective
Evaluate whether attacker-controlled content can manipulate the LLM’s behavior by overriding intended usage constraints, demonstrating prompt injection risk.
________________________________________
2. Threat Model
Attacker capabilities:
•	Controls input presented to the LLM (e.g., user messages, documents, chat content, retrieved data).
Security assumption under test:
•	The LLM should not follow instructions embedded inside untrusted content and should respect higher-level usage constraints.
________________________________________
3. Attack Description (High-Level)
An input was crafted and supplied as ordinary content.
When the model processed this content, it altered its behavior and violated intended control boundaries, demonstrating that it could not reliably distinguish trusted instructions from attacker-controlled text.
This represents an indirect prompt injection vulnerability.
________________________________________
4. Observed Impact
The LLM exhibited one or more of the following behaviors:
•	Followed attacker-controlled instructions embedded in content
•	Violated intended usage constraints
•	Disclosed internal/system-level information
•	Altered its operational behavior in unintended ways
Risk Severity: High
Because in real applications this could enable:
•	Data leakage
•	Policy bypass
•	Unsafe actions when connected to tools/agents
•	Business logic manipulation
•	Loss of trust in AI outputs
________________________________________
5. Root Cause Analysis
The LLM processes all context (system instructions, developer messages, user input, retrieved data) as a single text stream.
This makes it difficult for the model to enforce trust boundaries, allowing untrusted content to influence high-level behavior.
________________________________________
6. Mitigations & Recommendations
   - Strict separation of trusted instructions and untrusted content
   - Input sanitization and filtering for retrieved or user-provided data
   - Instruction hierarchy enforcement at the application level
   - Constrained tool permissions and human approval for sensitive actions
   - Monitoring and logging for instruction-override patterns
________________________________________
7. Conclusion
This assessment demonstrates that prompt injection remains a critical risk in modern LLM deployments.
Without strong architectural controls, attacker-controlled content can compromise the integrity, confidentiality, and safety of AI systems.
