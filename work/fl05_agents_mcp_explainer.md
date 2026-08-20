# FL-05 — Technical Explainer: Workflows vs Agents & Model Context Protocol (MCP)

- **Author:** Goutam (FlyRank ML Intern)
- **Track:** AI Fluency — FL-05 MCP & Agentic System Architecture
- **Date:** 2026-08-20

---

## 1. The Core Technical Distinction: Workflows vs. Agents

### What is a Workflow?
A **workflow** is a deterministic, pre-planned sequence of execution steps. In a workflow, the path of execution, control flow logic, data handoffs, and step order are hardcoded by human developers. While individual steps may utilize Large Language Models (LLMs) to transform or summarize text, the LLM does not decide *what step comes next*. If Step A succeeds, the system strictly proceeds to Step B. 

### What is an Agent?
An **agent** is an autonomous control loop where an LLM dynamically determines its own execution path, selects tools, evaluates intermediate outputs, and decides whether to continue, retry, or stop based on environment feedback. Rather than following a rigid DAG (Directed Acyclic Graph), an agent operates in an iterative **Reasoning → Action → Observation** loop (ReAct pattern).

### Classification of the FL-04 Pipeline
Our FL-04 pipeline (`01_prepare` → `03_train` → `04_evaluate` → `05_build_pdf`) is strictly a **Workflow**, not an agent. The execution path is hardcoded sequentially in `scripts/run_all.py`. The LLM does not autonomously decide whether to train a Random Forest vs Logistic Regression; it simply executes pre-configured code steps in fixed order.

---

## 2. Model Context Protocol (MCP) Fundamentals

The **Model Context Protocol (MCP)** is an open open-standard protocol (often described as the *"USB-C port for AI"* Protocol) that standardizes how LLM applications securely connect to external tools, databases, and local environments. Instead of writing custom API integration code for every tool, MCP provides three core primitives:

1. **Tools**: Executable functions that the LLM can invoke to perform side-effects or fetch dynamic data (e.g. `view_file`, `run_command`, `grep_search`).
2. **Resources**: Passive data sources exposed to the model (e.g. local file paths, database schemas, API endpoints).
3. **Prompts**: Pre-configured prompt templates exposed by the server to guide interaction patterns.

---

## 3. Evidence of MCP Working Setup (3 Tool Tasks)

We executed three real system tasks using native tool capabilities that plain text-chat cannot perform:

### Task 1: Direct Local File System Inspection (`view_file`)
- **Tool Executed**: `view_file(AbsolutePath="data/raw/content_refresh_anonymized.csv")`
- **Output**: Inspected exact raw CSV header bytes and verified 44 column schemas directly from local storage. Plain chat cannot inspect local disk files.

### Task 2: Automated Subprocess Command Execution (`run_command`)
- **Tool Executed**: `run_command(CommandLine="python scripts/run_all.py")`
- **Output**: Executed full pipeline end-to-end, generating `outputs/model_results.json` and logging Precision@50 results. Plain chat cannot execute code on a host machine.

### Task 3: Ripgrep Pattern Code Search (`grep_search`)
- **Tool Executed**: `grep_search(Query="precision_at_50", SearchPath="scripts")`
- **Output**: Searched codebase files for exact method occurrences across python modules. Plain chat cannot perform indexed regex searches across workspace directories.

---

## 4. Concrete Agent Upgrade for the FL-04 Pipeline

To transform our deterministic FL-04 workflow into an **Autonomous Agentic Pipeline**, we would add an iterative evaluation loop:

```text
[Data Input] ---> [Agent Reasoning Loop] <---> [Tools: Train, Evaluate, Feature Audit]
                        |
            (Check: Precision@50 >= 0.700?)
              /                      \
      [Yes: Export PDF]      [No: Re-sample & Retrain]
```

### Proposed Agent Architecture Upgrade:
1. **Autonomous Evaluation Loop**: After training, the agent inspects `model_results.json`. If `Precision@50 < 0.700`, the agent autonomously diagnoses the cause (e.g. low feature depth or class imbalance).
2. **Dynamic Tool Calling**: The agent dynamically invokes hyperparameter tuning tools (`train_model(max_depth=15)`), adds new engineered features, or requests fresh dataset slices from HuggingFace without human intervention.
3. **Self-Correction & Stopping Condition**: The loop continues until `Precision@50 >= 0.700` is achieved, at which point the agent calls `build_pdf_report()` and posts the final summary.
