---
name: add-or-update-api-endpoint-with-ui-and-tests
description: Workflow command scaffold for add-or-update-api-endpoint-with-ui-and-tests in agent-zero.
allowed_tools: ["Bash", "Read", "Write", "Grep", "Glob"]
---

# /add-or-update-api-endpoint-with-ui-and-tests

Use this workflow when working on **add-or-update-api-endpoint-with-ui-and-tests** in `agent-zero`.

## Goal

Implements a new API endpoint or updates an existing one, integrates it with the frontend UI, and adds corresponding tests and documentation.

## Common Files

- `api/*.py`
- `api/*.py.dox.md`
- `helpers/*.py`
- `helpers/*.py.dox.md`
- `webui/components/**`
- `webui/js/**`

## Suggested Sequence

1. Understand the current state and failure mode before editing.
2. Make the smallest coherent change that satisfies the workflow goal.
3. Run the most relevant verification for touched files.
4. Summarize what changed and what still needs review.

## Typical Commit Signals

- Create or update an API handler in api/ (e.g., api/stop.py, api/rename_work_dir_file.py)
- Add or update API documentation (e.g., api/*.py.dox.md)
- Update or create related helper logic (e.g., helpers/*.py, helpers/*.py.dox.md)
- Update frontend UI logic and markup to use the new API (e.g., webui/components/*, webui/js/*, webui/index.html)
- Add or update tests to cover the new API and UI behavior (e.g., tests/test_*.py)

## Notes

- Treat this as a scaffold, not a hard-coded script.
- Update the command if the workflow evolves materially.