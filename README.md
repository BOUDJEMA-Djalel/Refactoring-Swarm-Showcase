# The Refactoring Swarm

An autonomous multi-agent system that takes a folder of poorly written Python code (buggy, undocumented, untested) as input and delivers a clean, functional, test-validated version as output — with no human intervention.

Academic project developed as part of the IGL (Software Engineering) module at ESI Algiers, 2025-2026.

---

## Scientific Context

This project is part of an Empirical Software Engineering research experiment. The objective goes beyond writing code: it involves designing an LLM-based agent architecture capable of performing software maintenance autonomously.

---

## System Architecture

The system orchestrates collaboration between three specialized agents:

**The Auditor**
Reads the source code, runs static analysis via Pylint, and produces a structured refactoring plan.

**The Fixer**
Takes the plan as input and modifies files one by one to correct identified errors.

**The Judge**
Runs unit tests (pytest) on the corrected code. On failure, it sends the code back to the Fixer with error logs — the Self-Healing Loop. On success, it confirms mission completion.

```
Buggy code  -->  Auditor  -->  Refactoring plan
                                      |
                                   Fixer
                                      |
                                   Judge
                              /           \
                           Fail          Success
                      (loop back)   (mission complete)
```

---

## Team Organization

The project involves four complementary roles within a team of 4 students:

| Role | Responsibilities |
|---|---|
| Orchestrator (Lead Dev) | Execution graph design (LangGraph / CrewAI / AutoGen), agent relay logic, main.py and CLI |
| Toolsmith | Python functions called by agents (internal API), sandbox security, pylint and pytest interfaces |
| Prompt Engineer | Writing and versioning system prompts, hallucination and token cost optimization, context management |
| Quality & Data Manager | Full telemetry, experiment_data.json logging, internal test dataset creation |

---

## Tech Stack

| Technology | Usage |
|---|---|
| Python 3.x | Main language |
| LangGraph / CrewAI / AutoGen | Agent orchestration |
| Pylint | Static code analysis |
| Pytest | Unit test execution |
| LLM API | Agent intelligence |
| JSON | Logging format (experiment_data.json) |
| Virtualenv | Environment isolation |

---

## Automated Evaluation Criteria

Evaluation is fully automated by a correction bot on a hidden dataset (minimum 5 unseen buggy code instances):

| Dimension | Weight | Criteria |
|---|---|---|
| Performance | 40% | Does the final code pass unit tests? Has the Pylint score improved? |
| Technical Robustness | 30% | Does the system run without crashing? No infinite loop (max 10 iterations)? --target_dir argument respected? |
| Data Quality | 30% | Is experiment_data.json valid? Does it contain the complete history? |

---

## Status

Project completed. Source code is kept private. This repository serves as a portfolio showcase for recruiters.

---

## Academic Context

Instructor: BATATA Sofiane — IGL Module, ESI Algiers, 1CS 2025-2026.
