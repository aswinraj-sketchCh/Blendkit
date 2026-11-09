# Blendkit — agent rules

Blender add-on (Python, runs inside Blender's interpreter) for searching, downloading, uploading and rating assets from the Blendkit service. Read [CONTRIBUTING.md](CONTRIBUTING.md) before changing anything.

## Layout
- Add-on modules live at the repo root (`__init__.py`, `search.py`, `download.py`, `upload.py`, `ui*.py`, …).
- `bk_client/` and `bk_proxor/` are separate components (`bk_proxor` is a git submodule: `git submodule update --init bk_proxor`). Formatters and linters exclude them.
- `lib/` is vendored; never edit or format it.
- `tests/` runs inside Blender (`blender --background`), not plain pytest.

## Checks (mirrors `.github/workflows/PR.yml`)
- `python -m pip install -r devs/requirements.txt`
- `python -m isort . --check-only --diff`
- `python -m black . --check --diff`
- `python dev.py build` → `out/blenderkit.zip`
- Python `>=3.10,<3.13`; keep `numpy<2`.

## Rules
- Blender API calls only on the main thread; network work goes through the client/task queue (`client_lib.py`, `tasks_queue.py`).
- Do not touch `addon_updater*.py` (third-party).
