# hr-self-service-poc

A proof-of-concept agentic workflow built in n8n. An employee asks a routine HR question; the agent looks up their record, reads the relevant policy, and answers — without HR needing to be in the loop.

**Live demo:** [hr-self-service-poc.onrender.com](https://hr-self-service-poc.onrender.com)  
**Project page:** [ancatrif.com/hr-agent](https://ancatrif.com/hr-agent/)

> All data is synthetic. 20 fictional employee records, made-up names and balances, no real company or HR system.

---

## What it does

1. Receives an employee ID and a question via webhook
2. Looks up the matching record in a Google Sheet (stand-in for an HRIS)
3. Assembles a system prompt with the employee's record + relevant policy text
4. Sends it to Claude Sonnet 4.6, instructed to answer only from what it was given
5. Returns the answer immediately, and logs the exchange to a separate sheet in parallel

---

## Stack

- **n8n** — workflow orchestration (webhook, Google Sheets, code node, Claude, logging)
- **Claude Sonnet 4.6** — answer generation
- **Google Sheets** — employee data (synthetic) + conversation log
- **Render** — hosting for the demo frontend

---

## What's deliberately missing

This is a PoC, not a production system. Things that would be required before touching real employee data:

- SSO authentication (employee ID is currently typed by hand)
- Live HRIS connection (Workday, BambooHR) instead of the Google Sheet
- Rate limiting on the webhook
- Audit logging tied to verified identity
- Vector retrieval for a larger policy library (5 short docs are inlined today; 50 would need RAG)

---

## The assumption being tested

Not "can AI answer HR questions" — that part is easy. The real question is whether employees accept the answers often enough that they don't immediately escalate to a human anyway. Everything else is secondary until that's confirmed.

---

## Author

Anca Trif · [ancatrif.com](https://ancatrif.com) · [LinkedIn](https://www.linkedin.com/in/ancatrif)
