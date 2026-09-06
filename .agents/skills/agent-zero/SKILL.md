```markdown
# agent-zero Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you the core development patterns, coding conventions, and workflows used in the `agent-zero` Python codebase. The repository is structured for modularity and extensibility, supporting backend API development, plugin/extension integration, and a modern web UI. All significant changes are expected to be accompanied by tests and documentation updates, ensuring reliability and maintainability.

## Coding Conventions

- **File Naming:**  
  - Python files use `camelCase` (e.g., `stopAgent.py`, `renameWorkDirFile.py`).
  - Documentation files follow the pattern `*.py.dox.md`.
  - Test files: `test_*.py`.
- **Imports:**  
  - Use absolute imports.
    ```python
    from helpers.fileUtils import readFile
    ```
- **Exports:**  
  - Use named exports (explicitly define what is exported from a module).
    ```python
    # helpers/myHelper.py
    def useful_function():
        pass

    __all__ = ['useful_function']
    ```
- **Commit Messages:**  
  - Freeform, sometimes prefixed with `fix`.
  - Concise (average 41 characters).

## Workflows

### Add or Update API Endpoint with UI and Tests
**Trigger:** When adding a new backend API feature that is exposed to the frontend and needs to be tested and documented.  
**Command:** `/add-api-endpoint`

1. **Create or update an API handler**  
   - Place in `api/` (e.g., `api/stop.py`).
2. **Add or update API documentation**  
   - Create or edit `api/*.py.dox.md`.
3. **Update or create related helper logic**  
   - Edit or add files in `helpers/` (e.g., `helpers/stopHelper.py`).
4. **Update frontend UI logic and markup**  
   - Update `webui/components/*`, `webui/js/*`, and `webui/index.html` as needed.
5. **Add or update tests**  
   - Cover the new API and UI behavior in `tests/test_*.py`.
6. **Update documentation**  
   - Edit `AGENTS.md` or `README.md` as needed.

**Example:**
```python
# api/stop.py
from helpers.stopHelper import stop_agent

def handle_stop(request):
    agent_id = request.json['id']
    stop_agent(agent_id)
    return {'status': 'stopped'}
```

### Add or Enhance Plugin or Extension with Contracts and Tests
**Trigger:** When introducing or improving a plugin/extension, ensuring it is well integrated and tested.  
**Command:** `/add-plugin`

1. **Create or update plugin/extension directory**  
   - Use `plugins/_plugin_name/`.
2. **Add API handlers, helpers, and config files**  
   - Place in `api/*.py`, `helpers/*.py`, `default_config.yaml`, `plugin.yaml`.
3. **Add or update prompts**  
   - Use `prompts/*.md` or `plugins/_plugin_name/prompts/*.md`.
4. **Implement or update frontend UI components and stores**  
   - Update `webui/components/**`, `webui/js/**`, or `plugins/_plugin_name/webui/**`.
5. **Add or update tests**  
   - Backend: `plugins/_plugin_name/tests/test_*.py`
   - Frontend: `tests/test_*.py`
6. **Update documentation**  
   - Edit `AGENTS.md`, `README.md`, or `.dox.md`.

**Example Directory Structure:**
```
plugins/_chatNaming/
  ├── api/
  ├── helpers/
  ├── prompts/
  ├── webui/
  ├── tests/
  ├── default_config.yaml
  └── plugin.yaml
```

### WebUI Bundling and Asset Delivery Enhancement
**Trigger:** When optimizing or extending the frontend asset delivery pipeline (e.g., adding a bundler, service worker, or manifest).  
**Command:** `/update-webui-bundling`

1. **Add or update helper scripts for bundling and serving assets**  
   - Edit `helpers/ui_bundler.py`, `helpers/ui_server.py`.
2. **Update or add service worker and asset delivery logic**  
   - Edit `webui/sw.js`, `webui/index.html`, `webui/js/extensions.js`.
3. **Update frontend startup logic**  
   - Modify `webui/index.html`, `webui/index.js`.
4. **Add or update tests for bundling and service worker behavior**  
   - Use `tests/test_ui_bundler.py`, `tests/test_webui_service_worker.py`, `tests/test_webui_startup_assets.py`.
5. **Update documentation**  
   - Edit `.dox.md`, `AGENTS.md`.

**Example:**
```python
# helpers/ui_bundler.py
def bundle_assets():
    # Logic to bundle JS/CSS assets for webui
    pass
```

### Add or Update Feature with Regression Tests and Docs
**Trigger:** When adding a new feature or fixing a bug, ensuring it is covered by tests and documented.  
**Command:** `/add-feature-with-tests`

1. **Implement or update feature logic**  
   - Backend: `helpers/*.py`
   - Frontend: `webui/js/*.js`, `webui/components/**`
2. **Add or update regression/unit tests**  
   - Use `tests/test_*.py`.
3. **Update documentation**  
   - Edit `AGENTS.md`, `README.md`, or `.dox.md`.

**Example:**
```python
# helpers/newFeature.py
def new_feature():
    return True

# tests/test_newFeature.py
from helpers.newFeature import new_feature

def test_new_feature():
    assert new_feature() is True
```

## Testing Patterns

- **Test Framework:** Unknown (likely `pytest` for Python).
- **Test File Pattern:**  
  - Python: `tests/test_*.py`
  - (Legacy/Other: `*.test.ts` for TypeScript, but not primary here)
- **Test Structure:**  
  - Place tests alongside or within a `tests/` directory.
  - Cover both backend (Python) and frontend (JS/TS) logic as appropriate.
- **Example:**
    ```python
    # tests/test_stopAgent.py
    from api.stop import handle_stop

    def test_handle_stop():
        req = type('obj', (object,), {'json': {'id': 1}})
        resp = handle_stop(req)
        assert resp['status'] == 'stopped'
    ```

## Commands

| Command                  | Purpose                                                         |
|--------------------------|-----------------------------------------------------------------|
| /add-api-endpoint        | Add or update an API endpoint, UI, tests, and documentation     |
| /add-plugin              | Add or enhance a plugin/extension with contracts and tests      |
| /update-webui-bundling   | Enhance WebUI asset bundling, delivery, and service worker      |
| /add-feature-with-tests  | Add or update a feature with regression tests and documentation |
```
