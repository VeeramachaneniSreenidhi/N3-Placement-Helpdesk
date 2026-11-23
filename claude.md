# CLAUDE.md — N3: Placement Helpdesk

## Context
Read `spec.md` first. This repository implements the **Placement Helpdesk** agent and MCP tools that answer student policy and drive questions strictly from provided documents with citations, say `"I don't know"` when information is absent, and build/save grounded prep plans.

## Folder Structure
- `spec.md` — Product, tool, guardrail, eval, attack, and demo specification.
- `CLAUDE.md` — Repository conventions and instructions for Claude Code.
- `data/policies.json` — Sample placement policy documents.
- `data/drives.json` — Sample company drive records.
- `src/mcp_tools/` — MCP tool implementations (`search_policy`, `get_drive`, `make_prep_plan`, `save_plan`).
- `evals/` — 35-case evaluation dataset (30 answerable + 5 unanswerable) and runner script.
- `audit.jsonl` — Append-only audit log (gitignored).

## Coding & Agent Rules
- Keep tool functions deterministic and easy to test directly in Python before exposing via MCP.
- Enforce strict grounding: if a fact is not supported by the loaded policy/drive data, return `"I don't know"` rather than guessing.
- Validate inputs (e.g., `weeks` between 1 and 12, non-empty query) and write structured entries to `audit.jsonl`.
- Do not commit `.env` or personal/student PII.
