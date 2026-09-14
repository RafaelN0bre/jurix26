# Case viewer — read and verify a case without programming

From `solverJurix26/`:

```bash
uv run python scripts/run_app.py
ASPIC_APP_PORT=8010 uv run python scripts/run_app.py
```

The default address is http://127.0.0.1:8000. Use the second command if port 8000 is occupied. The viewer lists cases on the left and displays the selected case in five tabs. ASPIC+ notation is available behind the technical-representation control. Hash navigation identifies the case and tab, for example `#/case-005/conferencia`, so a specific view can be linked directly.

## Symbols and glossary

Formal codes such as `CrimeLatroc`, `r4`, `¬r0` and `CaFa_FugaPreso_MorteVitima` have dotted underlines. Hovering or focusing with Tab shows their meaning in ordinary Portuguese. Graph nodes expose the same explanation through the browser tooltip. Escape closes the tooltip. The case-vocabulary table at the end of Analysis provides the complete mapping.

The documentation is in English; original case vocabulary, source evidence and application labels retain their existing language.

## Overview

The overview shows the collection size, annotated dossiers versus paper reference cases, agreement with the court and dossiers that have not yet passed through formalization.

Each case row reports atoms, rules, tested causal questions, court agreement, availability of an LRC layer, automatic-check results and availability of the source dossier on disk.

## Analysis — conclusions and reasons

The analysis presents:

- The principal conclusion and facts recognized or rejected as causes.
- Constructed arguments labeled accepted, rejected or undetermined. Paths reaching the same conclusion are grouped; the conclusion survives if at least one path survives.
- Disputes showing who contests what, their grounds and whether the contestation succeeds. The attack relation determines the result.
- Case vocabulary explaining symbols and their roles as alleged facts, settled facts, derived links or outcomes.
- Causal comparison: NESS, cause-in-fact under Definition 4.3 and but-for causation under Definition 3.5, expressed as ordinary questions.
- Legal relevance under the ICAIL 2026 model when that layer exists.

## Perspectives — judgment as a dispute

This tab reconstructs who maintained what and which movement changed the result. It uses the argumentation/decision distinction discussed in Prakken's 2008 adjudication model. The displayed trace is a project reconstruction; consult the [historical audit](audits/adjudication-and-factors.md) before treating it as a faithful implementation of the entire dialogue model.

The adjudication map places each rule inside its author's box, grouped into adjudicators, parties and uncontested material. Solid red arrows show attacks; dashed gray arrows show support from one rule's conclusion to another's antecedent. Red ellipses identify defeated rules. Both CIF and LRC are represented so doctrinal defenses remain visible.

The argumentation trace starts with the parties and then admits each judge's rules in the recorded order, showing changes in causal verdicts. A concurring opinion can open another supporting route: the cause may remain NESS while ceasing to be a but-for cause.

The decision trace admits judges' LRC material step by step from the general presumption. The turning point marks when a claim surviving the facts ceases to survive the legal analysis. Unattributed defenses enter every step and do not appear as individual moves; their count is displayed to make that limitation visible.

## Dossier — the expert's reading of the judgment

This tab shows the original case summary, perspective reconstructions, disagreements, causal units and literal passages marked in the PDF before formalization.

Fields expose their linked passages in expandable sections. Passages are also grouped by page with a count of fields using each one. An unlinked selected passage is flagged because it may indicate unfinished annotation.

When the original dossier is unavailable, the viewer displays an available normalized run brief and explicitly identifies it as a brief rather than the original dossier. A brief from a model-based historical run is the text supplied to that model.

## Formalization — origin of each component

The formalization view provides the solver-versus-court comparison; atoms with meaning, type, status, role, author and evidence; rules with plain-language readings and evidence; and an LRC layer distinguishing solver-calculated bridge premises from doctrinal premises extracted from the judgment.

It also records modeling notes, open issues and available provenance, including source files, run IDs and, for historical model-based runs, model information and prompt hashes.

## Verification — confidence in the reconstruction

Four checks organize the view:

1. **Did the framework reach the court's conclusion?** Agreement counts and side-by-side readings for differences. A mismatch is a finding that identifies a rule or representation to review.
2. **Did formalization use the dossier?** Cited passages, reused dossier records and omitted source material, including passage text so the omission can be assessed.
3. **Can every component be traced to the judgment?** Atoms, rules and causal questions without supporting passage references.
4. **Does it pass automatic checks?** The deterministic `formalize.validate` report covers rule grammar, codes, existing literals, mutual rebuts without undercuts and LRC coherence.

Where historical model-based run data exists, the view also lists models, calls, repairs and token usage. Repeated repairs indicate that prompts may need revision; this does not describe the current deterministic transcription as a model pipeline.

## Data sources

| Content | Location |
| --- | --- |
| Annotated dossiers | `data/annotations/<annotator>/*.json`; `ASPIC_DOSSIER_ROOT` overrides the search root |
| Formalizations | `data/translated/<case>/case.json`; `ASPIC_TRANSLATED_DIR` overrides the directory |
| Validation | `data/translated/<case>/validation.json` |
| Runs and briefs | `data/translated/<case>/runs/<run-id>/` |
| Paper reference cases | `solverJurix26/src/cases/examples.py` |

The viewer rereads records from disk on requests; regenerated formalizations become available without restarting the application.

## API inspection

- `GET /api/cases`: collection and available case views.
- `GET /api/cases/{id}/raw`: case and validation JSON.
- `GET /api/cases/{id}/coverage`: verification metrics.
- `GET /api/cases/{id}/glossary`: symbol-to-reading mapping used by tooltips.
- `GET /api/cases/{id}/perspectives`: adjudication map and traces.
