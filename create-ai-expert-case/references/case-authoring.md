# Case authoring guide

The live `get_case_form_spec` response is the source of truth for field names, schemas,
limits, examples, and readiness. This guide defines the reasoning process and must not
be used as a stale duplicate of the form specification.

## Evidence discipline

Build a private working ledger before drafting:

- **Confirmed** — directly supported by an explicitly selected source or by the
  contractor's answer.
- **Contradictory** — sources disagree; ask rather than choose.
- **Unknown** — useful but unsupported; leave blank, phrase without the fact, or ask.
- **Forecast/target** — allowed only when labelled as a forecast or target, never as an
  achieved result.
- **Publishable image** — the contractor explicitly selected this exact image and it is
  safe to publish.

The ledger is local working context. Do not send it to MCP or persist it in the case.

Never derive a percentage, saving, ROI, volume, date, customer identity, testimonial, or
implementation detail unless the necessary inputs are present and the conclusion is
clearly supported. Do not silently resolve contradictions.

## What makes a substantive case

A strong case normally lets a reader understand:

1. Who had the problem and in what operating context, without exposing confidential
   details.
2. What happened before the project and why it mattered.
3. What was actually built or changed.
4. How the resulting workflow works and where human decisions remain.
5. What result is confirmed, how it was observed, and what limitations apply.
6. Which processes and interview questions make the case useful to a future lead.

Not every case has quantitative metrics. A precise qualitative result is better than an
invented number. Empty optional fields are acceptable when no evidence exists.

## Conditional brainstorm

Do not ask questions merely because optional fields are empty. Start a round only when
an answer could remove a blocker, resolve a contradiction, or materially improve the
reader's understanding or credibility.

Rank questions by expected value:

1. submission blockers and source contradictions;
2. problem and baseline context;
3. what changed and how the solution works;
4. confirmed outcomes and how they were measured;
5. constraints, human oversight, scale, and reusable process detail;
6. optional color such as a real quote or selected image.

Ask only 2–3 questions per round. Keep them concrete and answerable. Where useful,
offer response shapes without suggesting facts, for example: “Можно ответить без точных
цифр: что стало быстрее или надёжнее?”

After each round:

- update the draft immediately;
- validate again;
- mark answered issues as closed;
- choose the next 2–3 highest-value unresolved questions.

There is no numerical round limit. Stop when material opportunities are gone or the
contractor says there is no more information. Do not ask the same thing in different
words. Preserve unresolved warnings in the final summary.

## Images and privacy

Only upload an image after the contractor explicitly chooses it for publication. Inspect
the exact file locally first. Do not upload folders, source documents, hidden files,
screenshots containing personal data, or convenient nearby images.

The upload URL and its authorization header are temporary transport data. Do not quote
them in chat, write them to the case, or include them in a report. After finalization,
use only the returned media ID.

## Submission boundary

Draft creation and editing are autonomous. Submission is different:

- present the final version and validation outcome first;
- obtain an immediate explicit decision to submit this version;
- call `submit_case`;
- let the MCP elicitation collect the server-required confirmation;
- if the user declines, cancels, the client lacks elicitation, or the case changes during
  confirmation, leave the status unchanged and explain the next safe action.
