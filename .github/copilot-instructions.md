<!-- Copilot / AI agent helper for DeepLive.V10.24 -->
# Copilot instructions — DeepLive.V10.24

This file gives concise, actionable guidance for AI coding agents working in this repository.

1) Project overview
- Windows-focused GUI/Python app packaged with an embedded Python runtime under `_internal\python`.
- One-click entry: `Start.bat` (calls `_internal\setenv.bat` then runs `_internal\BenZi_Deep\start.py`).
- Persistent user data lives in the `userdata/` folder; screenshots and samples under `Screenshot/` and `samples/`.

2) Key files and components (quick map)
- `Start.bat` — primary launcher. Example run: call `_internal\setenv.bat` then execute the bundled Python.
- `_internal\setenv.bat` — sets `PYTHONEXECUTABLE`, `PYTHON_PATH`, `CUDA_PATH`, and manipulates `PATH`. Read before changing runtime behavior.
- `_internal\BenZi_Deep\start.py` — main application entry invoked by `Start.bat`.
- `_internal\python` — embedded Python runtime + `Scripts` and `Lib\site-packages` (treat as vendored dependency).

3) Developer/run workflow
- To run locally (dev):
  - Open a Windows shell in repo root.
  - Run: `_internal\setenv.bat` to configure environment variables.
  - Then run the packaged python directly, for example:
    `_internal\python\python.exe _internal\BenZi_Deep\start.py run BenZi_Deep --userdata-dir="%CD%\\userdata"`
- Avoid modifying `Start.bat` semantics unless you understand `setenv.bat` side-effects (PATH, HOME, TEMP override).

4) Patterns & conventions discovered
- The repo prefers self-contained, Windows-centric packaging (embedded interpreters, batch scripts) over system installs.
- Environment bootstrapping happens via `_internal\setenv.bat`; changes there affect all runtime paths.
- Vendorized libraries and caches live under `_internal` and `_internal\_z\u` (user-like home). Treat these as part of the runtime image.

5) Integration points & external dependencies
- CUDA: `_internal\CUDA` and its `bin` are wired into PATH via `setenv.bat`. GPU-dependent code expects CUDA in that location.
- PyQt6: `QT_QPA_PLATFORM_PLUGIN_PATH` set to the vendored PyQT6 plugin directory — don't move PyQt binaries without updating this variable.
- Windows-only: code and scripts assume Windows paths and environment variables (APPDATA, HOME overrides).

6) Editing guidance for AI agents
- Prefer small, targeted edits. If changing runtime behavior, update `_internal\setenv.bat` and verify `Start.bat` still launches.
- When adding Python deps, prefer placing them into `_internal\python\Lib\site-packages` or document steps to update the embedded runtime.
- Use explicit Windows paths in examples; run commands via PowerShell/CMD when testing.

7) Security & content note
- This project implements face-manipulation features. Follow platform policies and do not generate or assist with content that violates terms of service or local laws. When asked to implement features that could be abused, request explicit user justification and confirm policy compliance.

8) What an agent should do first
- 1) Read `_internal\setenv.bat` and `Start.bat` to understand the startup flow.
- 2) Run `_internal\setenv.bat` then invoke the bundled python with `_internal\python\python.exe _internal\BenZi_Deep\start.py run BenZi_Deep --userdata-dir="%CD%\\userdata"` to confirm runtime.
- 3) Inspect `userdata/` and `_internal` for any uncommitted large binaries before editing.

If anything here is unclear or you'd like more examples (run commands, common edit patterns, or a short checklist for safe changes), tell me which area to expand.
