# 🤖 Autonomous-Dev-Pipeline

**Autonomous-Dev-Pipeline** is an advanced multi-agent AI framework that simulates a professional software development department. By leveraging a tri-agent feedback loop, it moves beyond simple "chat" interactions and creates an autonomous system where AI agents write, test, and debug code via a local execution environment.

Unlike standard LLM interactions where the human must manually copy-paste errors, this system grants AI agents access to a terminal to self-correct until the code is production-ready.

---

## 🏗️ Architecture & Roles

The system is built on a **Specialized Agent** model. Each agent has a distinct system prompt and toolset to ensure a professional separation of concerns:

| Agent | Designation | Core Function | Input | Output |
| :--- | :--- | :--- | :--- | :--- |
| **The Coder** | Developer | Writes clean, modular Python code based on specs. | Requirements / Bug Report | `src/app.py` |
| **The Tester** | QA Engineer | Drafts rigorous `pytest` suites to validate logic. | Source Code | `tests/test_app.py` |
| **The Refactorer** | Senior Lead | Diagnoses stack traces and suggests surgical fixes. | Error Logs | Patch Instructions |

---

## 🔄 The Self-Correction Loop (The Agentic Cycle)

1.  **Drafting:** The **Coder** generates the initial script in the `src/` directory.
2.  **Validation:** The **Tester** creates a matching test suite and executes it via a subprocess.
3.  **Analysis:**
    *   **Success:** If all tests pass, the pipeline terminates and delivers the final code.
    *   **Failure:** The **Refactorer** intercepts the `stderr` output, identifies the root cause, and provides the **Coder** with a detailed fix report.
4.  **Iteration:** The loop restarts at Step 1, using the Refactorer's feedback to improve the code.

---

## 🛠️ Project Structure

```text
autonomous-dev-pipeline/
├── agents/             # System prompts and agent configurations
│   ├── coder.py        # Logic for the Development Agent
│   ├── tester.py       # Logic for the QA Agent
│   └── refactorer.py   # Logic for the Debugging Agent
├── workspace/          # The active execution environment
│   ├── src/            # Generated source code
│   └── tests/          # Generated unit tests
├── logs/               # Stored terminal outputs and error traces
├── main.py             # The Orchestrator (manages the loop state)
├── .env                # API Credentials (OpenAI/Anthropic/Local)
└── requirements.txt    # Project dependencies
```
