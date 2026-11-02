# 04: Document-grounded Q&A

**What to build:** A signed-in user can ask a free-text question about one of their uploaded documents and receive an answer grounded strictly in that document's own text, or an explicit refusal when the text doesn't support an answer.

**Blocked by:** 02

**Status:** ready-for-agent

- [ ] A user can submit a question against a specific library document
- [ ] A question answerable from the document's text returns a grounded answer
- [ ] A question with no basis in the document's text returns an explicit refusal, never a fabricated or general-knowledge answer
- [ ] The Q&A call goes through OpenRouter, never a direct model-provider call
