\# LLM SOC Monitoring



SOC monitoring and detection engineering for LLM applications.

Detects prompt injection, jailbreaks, and data-leak attempts using Wazuh SIEM,

mapped to OWASP LLM Top 10 and MITRE ATLAS.



\*\*Status:\*\* Week 1 complete (chatbot + structured logging). Week 2: Wazuh deployment and attack simulation.



\## Architecture



```mermaid

flowchart LR

&#x20; U\["User or attacker"] --> A\["HelpBot (Flask app)"]

&#x20; A --> O\["Ollama (local LLM)"]

&#x20; O --> A

&#x20; A --> L\["JSON logs (logs/chat.log)"]

&#x20; L --> W\["Wazuh agent"]

&#x20; W --> S\["Wazuh server and dashboard"]

&#x20; S --> R\["Custom detection rules"]

&#x20; R --> P\["Alerts and IR playbook"]

```



\## Project structure



\- `app/` - chatbot application (Flask + Ollama)

\- `logs/` - JSON logs (not committed to Git)

\- `rules/` - Wazuh detection rules

\- `playbooks/` - incident response playbooks

\- `docs/` - diagrams and write-ups



\## How to run



1\. Install \[Ollama](https://ollama.com) and pull a model (`ollama pull llama3.2:3b`).

2\. Create a virtual environment and install dependencies:

&#x20;  `python -m venv venv`, activate it, then `pip install -r requirements.txt`

3\. Start the app: `python app/app.py`

4\. Send a message:

&#x20;  `POST http://127.0.0.1:5000/chat` with JSON `{"message": "...", "user\_id": "...", "session\_id": "..."}`



\## Log format



Each interaction is written as one JSON line with: `timestamp`, `event\_type`, `app`, `user\_id`,

`session\_id`, `source\_ip`, `prompt`, `response`, `prompt\_length`, `response\_length`, `latency\_ms`.



\## Roadmap



\- \[x] Week 1: Chatbot with hidden system prompt and canary secret, structured JSON logging

\- \[ ] Week 2: Deploy Wazuh, ingest logs, simulate OWASP LLM Top 10 attacks

\- \[ ] Week 3: Detection rules, dashboard, MITRE ATLAS / OWASP mapping

\- \[ ] Week 4: Incident response playbook, testing, final report



\## Safety note



All testing is done against my own chatbot in a local lab. No real systems are targeted.

