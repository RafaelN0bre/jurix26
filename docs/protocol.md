# Minimum legal reconstruction protocol for causal analysis

## 1. Purpose

This protocol guides legal experts in reconstructing the positions in a Brazilian Supreme Court (STF) judgment concerning a general-repercussion issue. The reconstruction should be concise, traceable and legally faithful, providing sufficient input for a knowledge engineer to canonicalize, formalize and execute the case theory.

> The legal expert reconstructs what each perspective maintains, identifies relevant facts and causal relations, explains disagreements and links the passages supporting that reading.

Experts do not need to model logic, create graphs, manage technical identifiers or anticipate the computational representation.

## 2. Principles

### Perspective-based reconstruction

The primary working unit is a legal perspective. The usual order is appellant, respondent, reporting justice, concurring opinions with independent grounds, dissenting opinions and the STF's final position. Not every case contains every perspective.

### Minimum structure and legal authorship

The form includes only information needed for handoff. Fields without relevant content may be marked **Not identified** or **Not applicable**. Substantive reconstruction belongs to the legal expert; the tool organizes the record, preserves provenance and links selected passages to completed fields.

### Verifiable sources

Every relevant claim should be traceable to a passage in the full judgment. Where available, the platform records the document, PDF page, official page number, opinion or author, selected quotation and visual position automatically.

### Ordinary legal language

Experts may use terms such as candidate cause, legally relevant cause, causal relation, rejected cause, reason for rejection, point of disagreement and undecided issue. Translation into formal categories belongs to the knowledge engineer.

## 3. Expert workflow

```text
UNDERSTAND THE CASE
        ↓
RECONSTRUCT THE PERSPECTIVES
        ↓
IDENTIFY CAUSAL UNITS AND DISAGREEMENTS
        ↓
SUMMARIZE AND HAND OFF
```

The PDF remains accessible throughout as the primary source.

## 4. Step 1 — Case identification

Most fields may be populated administratively when a session is created and remain editable when necessary. This step should fit on one screen.

| Field | Entry |
| --- | --- |
| Case number | |
| Appellant | |
| Respondent | |
| General-repercussion issue | |
| Binding thesis established | |
| Adjudicating body | |
| Reporting justice | |
| Judgment outcome | |
| Judgment date | |

## 5. Step 2 — Reconstruction by perspective

This is the expert's main activity. For each perspective, the interface presents its form, the judgment PDF and passages already linked to that perspective. A PDF passage can be selected and linked directly to the field being completed.

### Appellant

| Field | Entry |
| --- | --- |
| Position defended | |
| Relevant facts invoked | |
| Legally relevant causes asserted | |
| Candidate causes asserted | |
| Causal relations asserted | |
| Main supporting passages | |

### Respondent

| Field | Entry |
| --- | --- |
| Position defended | |
| Relevant facts invoked | |
| Legally relevant causes contested | |
| Candidate causes contested | |
| Causal relations contested | |
| Main supporting passages | |

### Reporting justice

| Field | Entry |
| --- | --- |
| Relevant facts considered | |
| Legally relevant causes considered | |
| Candidate causes considered | |
| Causal relations considered | |
| Candidate causes rejected | |
| Causal relations rejected | |
| Reasons for rejection | |
| Undecided issues | |
| Conclusion | |
| Main supporting passages | |

### Concurring opinions with independent grounds

Create a record only when the opinion adds relevant grounds.

| Field | Entry |
| --- | --- |
| Justice | |
| Conclusion | |
| Independent grounds | |
| Candidate causes considered | |
| Legally relevant cause considered | |
| Causal relation considered | |
| Agreement with the reporting justice | |
| Distinguishing point | |
| Main supporting passages | |

### Dissenting opinions

| Field | Entry |
| --- | --- |
| Justice | |
| Conclusion | |
| Grounds | |
| Candidate causes considered | |
| Legally relevant cause considered | |
| Causal relation considered | |
| Point of disagreement | |
| Reason for disagreement | |
| Majority arguments addressed | |
| Main supporting passages | |

### STF — Final position

| Field | Entry |
| --- | --- |
| Candidate causes rejected | |
| Legally relevant cause recognized | |
| Legally relevant cause rejected | |
| Causal relations recognized | |
| Causal relations rejected | |
| Undecided issues | |
| Conclusion | |

Completion should be selective. Do not repeat content already recorded under another perspective when a simple reference suffices.

## 6. Step 3 — Causal units

After reconstructing the perspectives, record only causal units needed to represent relevant points of the judgment.

| Field | Entry |
| --- | --- |
| Readable ID | |
| Candidate cause | |
| Outcome | |
| Causal relation | |
| Conclusion supported | |
| Perspective / origin | |
| Status in the judgment | |
| Treatment by the Court | |
| Main supporting passages | |

A causal unit need not represent the entire case. It isolates a relation important enough to distinguish positions, grounds or outcomes.

## 7. Step 4 — Disagreements

Record disagreements relevant to understanding why perspectives reach different conclusions.

| Field | Entry |
| --- | --- |
| Readable ID | |
| Point of disagreement | |
| Perspective 1 | |
| Perspective 2 | |
| What perspective 1 maintains | |
| What perspective 2 maintains | |
| Reason for disagreement | |
| Effect on the conclusion | |
| Main supporting passages | |

The expert describes the disagreement in ordinary legal language. Subsequent technical classification belongs to the engineer.

## 8. Step 5 — Annotator summary

The summary is the handoff cover sheet and should fit on one screen.

| Field | Entry |
| --- | --- |
| Central issue | |
| Causal units | |
| Common premises | |
| Contested premises | |
| Prevailing conclusion | |
| Rejected conclusions | |
| Ambiguities | |
| Undecided issues | |

## 9. Provenance

Selecting a PDF passage must allow direct linking to a perspective field, causal unit, disagreement or summary field. The tool captures available provenance metadata automatically. The expert need not create a separate annotation record before using a passage as a source.

## 10. Engineer handoff

The handoff contains case identification, perspective reconstructions, causal units, disagreements, the annotator summary, linked passages with provenance and version history. The expert's submitted version is frozen after handoff.

The engineer canonicalizes expressions, separates similar concepts, chooses granularity, distinguishes events/states/actions/omissions, makes temporal relations explicit when needed, translates relations into formal structures, represents attacks/exceptions/scenarios and prepares the executable theory.

When a representation decision depends on legal interpretation, the engineer opens a focused clarification request for the expert.

## 11. Experiments with multiple legal experts

For a convergence study, all experts receive the same judgment and protocol version. Each works independently and sees only their own reconstruction and selected passages. Handoffs are frozen individually, and each dossier is canonicalized separately. Comparison begins only after the individual workflows end.

Comparison may consider reconstructed perspectives, candidate causes, causal relations, causal units, disagreements, conclusions, canonical specifications and solver results.

## 12. User experience rule

> Reconstruct in your own words what each position maintains. Identify the facts and causal relations that matter and link the passages supporting your reading. Finally, show where the positions disagree.

The expert interface should not require knowledge-engineering terminology or formal logic. Its purpose is to preserve the professional's legal expertise and minimize recording work while producing a traceable handoff.
