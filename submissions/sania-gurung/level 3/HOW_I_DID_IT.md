# How I Did It — Sania Gurung,
# Level 3, Track A

## What I did, step by step

I decided to build a meta-agent, an agent whose output is another agent. The idea came from reading the README carefully. The section on A2A says: "A2A tells you what exists, MCP lets you use it." Most people would build an agent that answers questions. I wanted to build one that produces agents that answer questions. That felt like actually understanding what A2A means in practice.

**Step 1 - Understanding the LPI tools**
I started by running `npm run test-client` and reading every tool's output carefully. I mapped each tool to a question I'd need to answer when generating a domain-specific agent: "What is the user's industry? What SMILE phase matters most? What does the knowledge base say about this domain? What have others done in this space?" Once I had that mapping, the architecture was obvious.

**Step 2 - Designing the provenance system first**
Before writing any LPI calls, I built the `Provenance` class. I wanted every piece of information the agent uses to be traceable to a specific tool call. This wasn't just for the requirement it's how I'd want to build any production AI system. An answer you can't explain is an answer you can't trust.

**Step 3 - Building the LPI query layer**
I called 5 of the 7 LPI tools in sequence:
- `smile_overview` - to understand the full framework before making domain decisions
- `query_knowledge` - with the user's description as the query
- `get_case_studies` - with auto-detected industry as the filter
- `get_insights` - with a full scenario string
- `smile_phase_detail` - with the auto-detected primary SMILE phase

I wrote `detect_industry()` and `detect_primary_phase()` as lightweight keyword mappers because I didn't want the meta-agent to depend on an LLM for its own decisions. The agent builder itself should be deterministic and fast.

**Step 4 - Building the code generator**
The hardest part was generating code that is actually readable and useful. I wanted the output file to be something a teammate could open and immediately understand - not generated garbage. So every section has a comment explaining why that LPI tool was chosen and what it returned. The `[SOURCE: LPI/tool_name]` annotation pattern appears both in the generated code and in the LLM prompt, so the generated agent's answers are also cited.

**Step 5 - Model recommendation**
I mapped domain keywords to Ollama models based on what I know about model strengths. Health and security domains benefit from `qwen2.5:5b`'s careful instruction-following. Manufacturing and smart cities use `llama3.2:3b` for faster inference on structured/IoT data. The recommendation is injected as a comment into the generated file so the user knows why that model was picked.

**Step 6 - A2A Agent Card**
The README mentions the bonus A2A Agent Card and says it "demonstrates you understand how agents discover each other." I wrote `agent.json` to accurately describe what the agent builder does, what it accepts, what it produces, and what LPI tools it uses. I also included the explainability methodology so any agent discovering this one knows it will get cited outputs.

---

## What problems I hit and how I solved them

**Problem 1 - MCP stdio transport is one-shot per subprocess call.**
The LPI server doesn't stay alive between calls — each `subprocess.run()` spins up a fresh node process. This means I had to send the full JSON-RPC request each time and parse the output fresh. I handled this by making `call_tool()` stateless: each call is independent, which actually makes the provenance tracking cleaner.

**Problem 2 - The server returns multiple JSON lines.**
I initially tried `json.loads(proc.stdout)` and it broke on multi-line output. Fixed by iterating line by line and matching on the request ID field.

**Problem 3 - Generated code with f-strings containing curly braces.**
When you use an f-string to generate Python code that itself uses f-strings, the inner braces need to be doubled (`{{` and `}}`). This caused silent formatting bugs in the first draft. I caught it by actually running the generated file and reading the syntax errors carefully.

**Problem 4 - Industry detection edge cases.**
"Smart building" contains "building" which I had mapped to "real_estate", but also relates to "energy" and "smart_cities". I resolved this by ordering the keyword checks so more specific terms (like "smart") take priority over generic ones ("building"). Not perfect, but honest — I documented the limitation.

---

## What I learned that I didn't know before

I hadn't worked with MCP before this. I knew about tool-calling in general from building the Symbiotex pipeline, but the stdio transport approach where the server is a subprocess you talk to with JSON-RPC over stdin/stdout was new to me. It's simpler than I expected, and I can see why it's a good standard for local agent tooling.

I also learned something about explainability that I hadn't thought about explicitly before. In Symbiotex, I generated structured JSON reports. But the report didn't explain *why* the threat was assessed a certain way — it just stated the confidence score. After reading SMILE and the evaluation criteria here, I realised that a confidence score without a source trace is just a number. The citation system I built for this agent is something I'm going to bring back to Symbiotex.

The A2A concept also clicked in a way it didn't when I first read the README. A2A isn't just a discovery protocol, it's a contract. When an agent publishes an Agent Card, it's saying "here is what I do, here is what I accept, here is what I guarantee about my output." That's the same principle as a well-documented API, just for agents. Writing `agent.json` made that concrete.

Signed-off-by: Sania Gurung <saniagurung5452@gmail.com>
