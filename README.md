<<<<<<< HEAD
# LogShield

LogShield is an offline PySide6 desktop application for importing and analyzing local SSH authentication logs. It stores normalized events in SQLite, detects brute-force bursts with the specified per-IP sliding window, supports incident review, and exports CSV/JSON reports. All sample records are synthetic.

## Requirements

- Python 3.11 or 3.12 (64-bit)
- PySide6
- SQLite (included with Python)
- Matplotlib
- pytest for development

Third-party versions are pinned in `requirements.txt` and `requirements-dev.txt`.

## Set up

Windows PowerShell:

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
```

Use `py -3.11` if that is the team's selected version. macOS/Linux can create the environment with `python3.12 -m venv .venv` and activate `.venv` using the platform's shell command.

## Generate the synthetic sample files

```powershell
python scripts\generate_logs.py
```

This creates `data/auth_sample.log` (over 1,000 lines across two days, attack bursts, a near miss, malformed records and the worked example) and `data/duplicate_check.log` for duplicate-import demonstration. Both are fictional and use documentation address ranges.

## Run

```powershell
python main.py
```

The database is created automatically at `data/logshield.db` on first launch. To rebuild it, close the application and remove that local database file; the next launch recreates the schema. `data/logshield.db` is local working data and is excluded from Git.

`python main.py --demo-data` opens the isolated synthetic UI preview. Demo history is read-only and is not written to the application database.

## Tests

```powershell
python -m pytest
```

The tests cover the parser, sliding-window rules and boundaries, event isolation, imports and duplicates, persistence constraints, incident review, report export, and the four-screen UI.

## Application structure

- `app/ui/`: the four primary screens and shared PySide6 components.
- `app/services/`: import worker and application workflows; services contain no Qt widget code.
- `app/algorithms/`: pure log parsing and per-IP sliding-window detection.
- `app/database/schema.sql`: SQLite schema and constraints.
- `app/database/connection.py`, `repositories.py`: connection lifecycle and parameterized persistence queries.
- `app/models/`: plain service request/response contracts and domain records.
- `scripts/generate_logs.py`: fixed-seed synthetic sample generation.

## Required workflow scope

The app supports local `.log`/`.txt` import up to 20 MB, SHA-256 duplicate prevention, malformed-line review, AND-combined paged event filters, per-IP summaries, threshold/window detection, persistent run history, incident evidence and review, a selected-run HIGH-only display filter, and CSV/JSON exports. Detection runs use thresholds 3–20 and windows 1–60 minutes. A same-IP successful login within the configured window after an incident raises severity to HIGH and is linked as evidence.

The application performs offline defensive analysis only. It does not capture live traffic, connect to external services, or use real authentication data.

## Submission documents

- `docs/TNN_LOGSHIELD_technical.pdf` — four-page architecture, schema, algorithm, worked example, and verification notes.
- `docs/TNN_LOGSHIELD_presentation.pdf` — six-slide live-demo presentation.
- `screenshots/` — four-screen captures and responsive UI review states.

=======
# LogShield-
>>>>>>> origin/main
