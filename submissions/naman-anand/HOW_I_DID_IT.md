# HOW I DID IT - Level 2 (Track E)

**Contributor:** Naman Anand
**Track:** QA & Security

## Step-by-Step Methodology

1.  **Environment Setup:** I cloned the repository and initialized the environment using `npm install`. I encountered a small delay with dependencies due to network speed, so I used the `--prefer-offline` flag as suggested in the troubleshooting guide.
2.  **Validation & Proof of Work:** I ran `npm run test-client` to ensure the baseline was stable. All 8/8 tools passed, confirming the MCP server logic was sound. I captured this raw terminal output and saved it in `test_output.txt` for automated verification.
3.  **Manual Fuzzing:** Instead of just running automated tests, I manually invoked the server using `node dist/src/index.js`. I focused on "Black Box" testing sending inputs that the developers likely didn't expect, such as SQL injection strings (`DROP TABLE`), malformed JSON, and empty objects.
4.  **Information Gathering:** I analyzed the error outputs. I noticed that while the tools are read only, the server's error handling reveals internal directory structures, which I documented as a security finding in my bug report.

## Problems Encountered & Solutions

* **SSH Permission Issue:** Initially, I couldn't clone the repo via SSH (`Permission denied`). I realized my local SSH key wasn't linked to GitHub. I solved this by switching to the HTTPS protocol for a faster setup.
* **Server "Hanging":** When I sent non-JSON text, the server stopped responding. At first, I thought my terminal crashed, but I realized it was a protocol mismatch where the server waits indefinitely for a valid JSON-RPC frame.
* **Automated Evaluation Fix:** During the initial PR check, the bot did not detect the test passes. I solved this by creating a dedicated `test_output.txt` file containing the piped output of the test client.

## Lessons Learned

* **MCP Protocol:** I learned how Model Context Protocol (MCP) servers handle standard input/output (stdio) for agent communication and how sensitive they are to malformed frames.
* **SMILE Rigor:** I learned that Digital Twins require a "Reality Emulation" phase. From a security perspective, this taught me that understanding the current 'as-is' state of a system is the first step in protecting it.
