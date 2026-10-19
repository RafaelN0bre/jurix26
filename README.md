# jurix26

Research repository for the JURIX 2026 project on legal annotation and executable causal argumentation. It contains the annotation application and ASPIC+ solver as Git submodules, with shared documentation, bibliography and local case data.

The case study is RE 608.880/MT (STF Theme 362), concerning state liability for a crime committed by an escaped prisoner. The formalization separates cause-in-fact (CIF) from legally relevant cause (LRC) and runs them in the CIF → LRC order.

## Repository structure

| Directory | Contents |
| --- | --- |
| `anotadorJurix26/` | JurisForm annotation application, evidence provenance and versioned handoff |
| `solverJurix26/` | ASPIC+ solver, causal analysis, formalization and case viewer |
| [docs/](docs/README.md) | Annotation protocol, modeling documentation and manual case theory |
| [bib/](bib/index.md) | Reference PDFs and their application in the project |
| [data/](data/README.md) | Local database, source dossiers and generated case records |

## Installation

Requirements: Git, Python 3.11 or later, `uv`, and Node.js with npm.

Clone `jurix26` with its submodules:

```bash
git clone --recurse-submodules https://github.com/RafaelN0bre/jurix26.git
cd jurix26
```

For an existing clone:

```bash
git submodule update --init --recursive
```

Run `uv sync` in each submodule. Run `npm install` in `anotadorJurix26/frontend/`.

## Annotation application

From `anotadorJurix26/`, start the backend:

```bash
uv run uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```

From `anotadorJurix26/frontend/`, start the frontend in a separate terminal:

```bash
npm run dev
```

Open http://localhost:5173 and load a session YAML through the administration interface. Users and credentials are defined by the session and backend configuration. The [annotation protocol](docs/protocol.md) specifies reconstruction and handoff.

## Formalization and analysis

From `solverJurix26/`:

```bash
uv run python scripts/build_case003_final.py
uv run python scripts/run_translated.py
uv run python scripts/generate_graphs.py
uv run python scripts/render_translated.py
```

The transcription script reads the [manual case theory](docs/formalizacao-caso003.md). Case records are written to `data/translated/`, HTML reports to `docs/graphs/`, and figures to `docs/figures/`.

Start the case viewer:

```bash
uv run python scripts/run_app.py
```

Open http://127.0.0.1:8000. Use `ASPIC_APP_PORT=8010 uv run python scripts/run_app.py` when the annotation backend occupies port 8000.

Run the solver tests:

```bash
uv run python -m pytest tests/ -q
```

## Data and configuration

Both submodules use the root `docs/` and `data/` directories by default.

| Variable | Purpose |
| --- | --- |
| `JURIX_WORKSPACE` | Solver workspace root |
| `ASPIC_TRANSLATED_DIR` | Formalized case directory |
| `ASPIC_DOSSIER_ROOT` | Source dossier search root |
| `JURIX_DATA_DIR` | Annotation database and uploads directory |
| `DATABASE_URL` | Annotation database connection |

Databases, uploads, annotation exports, backups, snapshots and generated reports are excluded from Git. Source dossiers must be supplied locally for dossier views. Documentation and bibliography are versioned.
