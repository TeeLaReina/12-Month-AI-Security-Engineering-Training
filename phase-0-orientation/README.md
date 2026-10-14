# Phase 0 - Orientation (6 – 19 October 2026)

**Status:** in progress

No cloud infrastructure is created in Phase 0. Everything runs on free compute and free accounts.

## Track A - AI

- [x] Hugging Face account
- [x] Kaggle account (free GPU)
- [x] Google Colab access confirmed
- [ ] Python refresher: numpy, pandas, Jupyter
- [ ] Gaming PC GPU model and driver recorded

## Track B - Cloud

- [x] Google Cloud account (existing)
- [x] Azure: free services recorded (12-month free services active until 13 Sep 2027; none in use)
- [ ] DigitalOcean access confirmed (nothing created)
- [x] Entra ID tenant baseline documented: see [entra-tenant-baseline.md](entra-tenant-baseline.md)
- AWS: deliberately deferred until Track B needs it

## Repo and tooling

- [x] Repository created
- [x] Git installed and configured on the Ubuntu laptop (noreply email, `main` as default branch)
- [x] SSH key added to GitHub for the Ubuntu laptop
- [x] GitHub Projects board created, linked to the repo and made public
- [ ] Git set up on the Windows gaming PC

## Community

- [x] garak Discord
- [x] OWASP GenAI Security Project Slack (#project-genai)
- [x] Azure Nigeria Community (Meetup)
- [x] Hacker Proof HQ (LinkedIn follow; no private community)

## Reading (orientation level)

- [x] OWASP GenAI LLM Top 10 2026 - first pass
- [x] MITRE ATLAS - introduction
- [x] NIST AI Risk Management Framework - overview

## Notes

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
