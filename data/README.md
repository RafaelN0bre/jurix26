# Research data

Shared storage for the annotation application and solver. Directory contents are excluded from Git, except for this README.

| Path | Contents |
| --- | --- |
| `jurix.db` | Annotation database |
| `jurix.db-wal`, `jurix.db-shm` | SQLite journal and shared-memory files |
| `uploads/` | Source judgment PDFs |
| `annotations/<annotator>/` | Expert dossiers, consolidation files and source documents |
| `annotations/translated/` | Historical formalization records and run artifacts |
| `consolidacao-main.json` | Consolidated dossier used by the case catalog |
| `translated/<case>/case.json` | Executable case record |
| `translated/<case>/validation.json` | Deterministic validation and solver–court comparison |
| `translated/<case>/runs/` | Run briefs, prompts, traces and intermediate records |
| `snapshots/` | Annotation-interface screenshots |
| `backup/` | Database snapshots and raw exports |
| `archive/` | Archived working material |

Judgment quotations and annotator statements retain their source language. Source dossiers must be supplied locally for dossier views; paper reference cases are included in the solver.

`ASPIC_DOSSIER_ROOT` selects the dossier search root. `ASPIC_TRANSLATED_DIR` selects the executable case directory. The annotation application uses `JURIX_DATA_DIR` for database and upload storage, and `DATABASE_URL` for the database connection.

The transcription and rendering commands are listed in the [repository README](../README.md).
