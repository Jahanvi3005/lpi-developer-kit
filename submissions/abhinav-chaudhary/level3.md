# Level 3 Submission — Abhinav Chaudhary

## 🚀 Overview

I built a simple AI agent that simulates how an LPI agent works by analyzing a user query, selecting relevant tools, and combining their outputs into a structured response.

Instead of directly calling the MCP server, I focused on designing the **core agent workflow** — tool selection, aggregation, and explainable output.

---

## 🧠 Architecture

User Input → Query Analysis → Tool Selection → Tool Execution → Aggregation → Final Response

---

## ⚙️ LPI Tools Used (Simulated)

### 1. get_case_studies

* Purpose: Provide real-world examples
* Output: Returns a case-study style explanation of the query

### 2. query_knowledge

* Purpose: Provide conceptual understanding
* Output: Returns theoretical explanation based on LPI concepts

### 3. smile_overview

* Purpose: Provide high-level SMILE methodology overview

---

## 🔄 Agent Flow

1. User inputs a question
2. Agent analyzes keywords in query
3. Selects relevant tools dynamically
4. Calls each tool
5. Collects outputs
6. Combines into structured answer

---

## 💡 Design Decisions

* Ensured at least **2 tools are always used**, even for vague queries
* Structured output into **reasoning, answer, and sources** for explainability
* Kept implementation simple and stable by avoiding external dependencies
* Focused on **agent orchestration logic rather than just output generation**

---

## 🛡️ Error Handling (Added After Feedback)

Based on feedback, I improved robustness by:

* Validating user input (handling empty input cases)
* Adding try/except blocks to prevent crashes
* Handling failures during tool execution and result processing

This ensures the agent behaves more like a real system and doesn’t break on unexpected input.

---

## 🔧 Limitations

* Current implementation uses **simulated LPI tools**, not real MCP calls
* Tool selection is keyword-based, not LLM-driven
* No persistent memory or multi-turn context

---

## 🔧 What I Would Improve

* Integrate real MCP-based LPI tool calls
* Use LLM-based reasoning for smarter tool selection
* Add context memory for multi-turn conversations
* Improve error logging and observability

---

## 💻 Repository

https://github.com/abhichaudhary256-sudo/lpi-agent-abhinav.git

---

## ▶️ How to Run

```bash
pip install -r requirements.txt
python agent.py
```

---

## 📌 Example

**Input:** What is SMILE?

**Output:**

* Case Study: Real-world implementation of SMILE
* Knowledge: Explanation based on LPI methodology

---

## 🧠 Key Learning

This project helped me understand how an AI agent is not just about generating answers, but about:

* selecting the right tools
* combining multiple sources
* and explaining how the answer was formed

---

## ✅ Checklist

* [x] Built custom agent
* [x] Uses multiple tools
* [x] Structured output
* [x] Explainability included
* [x] Error handling added
* [x] Separate repo created

Signed-off-by: Abhinav Chaudhary
