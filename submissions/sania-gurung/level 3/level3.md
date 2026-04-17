# Level 3 Submission — Sania Gurung

**Track:** A — Agent Builders
**GitHub repo:** https://github.com/SANIAGRG/lpi-agent-builder

---

## What I Built

**Agent Builder Agent** — a meta-agent that generates customised LPI agents.

Most agents answer questions. This agent's output is another agent.

You give it a digital twin use case. It queries 5 LPI tools, detects your
industry and primary SMILE phase, recommends an Ollama model, and generates
a ready-to-run `agent.py` tailored to your domain — with every decision
explained and cited back to the LPI tool that informed it.

---

## How to Run It

```bash
git clone https://github.com/SANIAGRG/lpi-agent-builder.git
cd lpi-agent-builder

# No pip install needed — stdlib only

python agent_builder_agent.py "health monitoring twin for ICU patients"
python agent_builder_agent.py "smart building energy optimisation"
python agent_builder_agent.py "crop yield prediction for wheat farmers"
```

---

## LPI Tools Used (5 of 7)

| Tool | Role in the agent |
|------|-------------------|
| `smile_overview` | Maps the use case to SMILE phases |
| `query_knowledge` | Retrieves domain-specific knowledge |
| `get_case_studies` | Finds relevant industry examples |
| `get_insights` | Gets scenario-specific advice |
| `smile_phase_detail` | Deep-dives the most relevant phase |

Every result is tracked in the provenance log printed after each run.

---

## Requirements Met

- [x] Accepts user input (digital twin description)
- [x] Queries at least 2 LPI tools (queries 5)
- [x] Processes results — synthesises into generated code
- [x] Cites which LPI tools and data were used — full provenance log + inline `[SOURCE: LPI/tool_name]` comments in every generated file
- [x] A2A Agent Card included (`agent.json`) — bonus

---

## Explainability

Every section of the generated agent contains:
```python
# [SOURCE: LPI/query_knowledge] — domain knowledge for healthcare
# [SOURCE: LPI/get_insights] — implementation advice for this scenario
```

The builder agent prints a full provenance summary:
```
📚 PROVENANCE — Every decision traced to its LPI source
[1] Tool: smile_overview     Finding: Full SMILE methodology...
[2] Tool: query_knowledge    Finding: Domain knowledge entries...
[3] Tool: get_case_studies   Finding: Case studies for healthcare...
[4] Tool: get_insights       Finding: Implementation advice...
[5] Tool: smile_phase_detail Finding: Phase data_integration detail...
```

Signed-off-by: Sania Gurung <saniagurung5452@gmail.com>
