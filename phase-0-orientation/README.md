### 9 October 2026 - Week 1, OWASP GenAI LLM Top 10 (2026)

**What I did**
- Read the OWASP GenAI LLM Top 10 2026 (first pass, no notes)
- Worked through recall, look-alike comparisons, three real-incident scenarios, a troubleshooting drill and a control trade-off exercise

**What I learned**
- Many AI security concepts sound alike and blur together fast. The only fix I've found is to digest each one on its own, then compare them side by side.
- **Prompt injection vs data poisoning -** the difference is *when and where*. Prompt injection happens at runtime - the model receives malicious instructions through text, an image, audio or a document, intentionally or not, and it usually affects that one interaction. Data poisoning happens earlier, in the data the model learns from or retrieves (training data, fine-tuning data or a RAG knowledge source). Because the corruption sits in that data, every user whose question touches it gets the same bad answer.
- **Sensitive information disclosure vs hidden context exposure -** ask *whose* information leaked. Sensitive information disclosure is data about people or the business - PII (personally identifiable information), PHI (protected health information), credentials, trade secrets, confidential files. Hidden context exposure is information about the model itself - its system prompt, the rules it was given, its guardrail logic. Attackers want that so they can understand how the system works and craft attacks that get around it.
- **Technique vs impact -** the technique is *how* an attack happens; the impact is *what it achieves*. When Bing Chat's rules leaked in 2023, the technique was prompt injection but the risk was hidden context exposure. The OWASP list mixes both kinds of item, which is exactly why it's easy to confuse them. Telling them apart matters for understanding intent, troubleshooting and choosing the right fix.
- **Indirect prompt injection through an untrusted RAG source -** RAG (retrieval-augmented generation) is when a chatbot searches a set of sources, such as company policy documents or customer reviews, and uses what it finds to answer. If one of those sources accepts content from anyone, an attacker can hide instructions inside it. In my drill, white-on-white text in a customer review told the bot to send customers to a fake refund site. The model itself never changed. It simply read the review and followed the hidden instructions. The fault was in what the model reads, not in the model.

**Key takeaways**
- Identifying the technique helps narrow down the intent, malicious or accidental, and that shapes how you triage, fix and test.
- Every control has a bypass. Weigh the risk you accept against the cost of running the control, the effort to maintain it and how well it works. That narrows the choice quickly.
- Not every incident is intentional, and not every attacker is external. Log what the AI retrieves and what it outputs, so you can trace a bad answer back to its source.

**Real-world link**
- Barracuda (7 Oct 2026) - phishing emails hiding prompt injections aimed at AI inbox assistants
