# Repository Guidelines


## Project Structure & Module Organization
This repository is a small `src`-layout Python package. Core library code lives in `src/televuer/`: `televuer.py` exposes the XR/Vuer runtime, and `tv_wrapper.py` provides the higher-level data wrapper and transforms. Public imports are re-exported from `src/televuer/__init__.py`. Manual integration scripts live in `example/` as `test_televuer.py` and `test_tv_wrapper.py`. Top-level docs and packaging metadata are in `README.md` and `pyproject.toml`.

## Build, Test, and Development Commands
Use a Python 3.10+ environment.

- `pip install -e .`: install the package in editable mode for local development.
- `pip install .`: install a non-editable local build.
- `python example/test_televuer.py`: run the direct `TeleVuer` integration script.
- `python example/test_tv_wrapper.py`: run the wrapper-based integration script.

These scripts expect an XR headset on the same network and, for streaming scenarios, a running `teleimager` server.

## Coding Style & Naming Conventions
Follow the existing Python style: 4-space indentation, module names in `snake_case`, classes in `PascalCase`, and methods/functions in `snake_case`. Keep argument names consistent with the public API (`use_hand_tracking`, `display_mode`, `webrtc_url`). Preserve the current docstring-heavy style for constructor behavior and coordinate-frame assumptions. No formatter or linter is configured in this repo, so keep edits minimal and consistent with surrounding code.

## Testing Guidelines
There is no formal `pytest` suite yet; testing is currently manual and hardware-aware. Add new verification scripts under `example/` and name them `test_<feature>.py`. Prefer small, runnable checks that exercise one workflow at a time. When changing networking, certificates, or XR data transforms, document the exact device/setup assumptions in the script or PR.

## Commit & Pull Request Guidelines
Recent history uses short, imperative commits, sometimes with prefixes such as `[fix]`, `[rename]`, and `[upgrade]` (for example, `[fix] README`). Keep commit subjects concise and focused on one change. PRs should include a clear summary, linked issue or context, manual test steps, and screenshots/log snippets when UI, XR display modes, or device connectivity behavior changes.

## Security & Configuration Tips
Do not commit generated certificates or local IP addresses. Prefer `XR_TELEOP_CERT` and `XR_TELEOP_KEY`, or `~/.config/xr_teleoperate/`, for local SSL material. Review any hard-coded host values in `example/` before sharing changes.
