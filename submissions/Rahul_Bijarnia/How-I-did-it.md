HOW I DID IT — Level 3 Agent (Rahul Bijarnia)
Steps I Followed
Ran the LPI sandbox locally on my system
Used the provided agent.py as the base implementation
Installed Ollama and configured a local LLM
Executed the agent using a test query through the terminal
Verified that multiple LPI tools (smile_overview, query_knowledge, get_case_studies) were being called
Observed how the LLM processed and combined results from different tools to generate a final answer
Problems I Faced
PowerShell blocked npm scripts initially due to execution policy restrictions
Ollama was not installed, causing connection errors
Missing Python dependencies such as requests
How I Solved Them
Changed execution policy in PowerShell to allow script execution
Installed Ollama and ensured the server was running properly
Installed required Python packages using pip install requests
What I Learned
How AI agents integrate multiple tools to solve complex queries
Importance of combining structured tool data with LLM-generated responses
How explainability improves trust and usability in AI systems
