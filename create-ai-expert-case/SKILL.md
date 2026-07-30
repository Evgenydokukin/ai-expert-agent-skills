---
name: create-ai-expert-case
description: Create or improve an ai-expert.pro contractor case from user-selected local files, notes, images, and answers through the contractor MCP. Use when a contractor asks Codex or Claude Code to prepare, edit, validate, strengthen, or submit their own case while keeping source files local.
---

# Create ai-expert.pro Case

Create the strongest truthful case supported by the contractor's materials. Keep every
source file local. Send to GD only the final case content and images the contractor
explicitly selects for publication.

Read [references/case-authoring.md](references/case-authoring.md) before authoring.

## Workflow

1. Confirm the `ai-expert` contractor MCP is connected and exposes
   `get_case_form_spec`. If case tools are missing, explain that the OAuth connection
   must be revoked and connected again with the new case scopes.
2. Call `get_case_form_spec` on every run. Treat its schemas, limits, field guidance,
   and readiness rules as authoritative. Then call `list_case_industries`.
3. Read only the files, notes, images, or directories the contractor explicitly names.
   Do not search their computer or broaden the requested directory. Do not upload
   source documents.
4. Separate:
   - confirmed facts;
   - contradictions that need a question;
   - missing information;
   - selected publishable images.
5. Create a new draft with `create_case`, or load the specified case with `get_case`.
   Fill or update known fields, `doc_json`, processes, and questions without asking for
   approval for each write. Use `update_case`, `replace_case_processes`, and
   `replace_case_questions`.
6. For each image explicitly selected for publication:
   - inspect its MIME and exact byte size locally;
   - call `begin_case_image_upload`;
   - upload only that file to the returned short-lived URL using the returned method
     and headers;
   - call `finalize_case_image_upload`;
   - reference the returned `media.id` in the cover or document.
   Never copy a local path, upload URL, or upload authorization header into the case text.
7. Call `validate_case`.
8. If the case is complete and substantive, do not start a questionnaire. If validation
   or the evidence shows a meaningful gap or a valuable strengthening opportunity, ask
   the 2–3 highest-value questions in one short round.
9. After every answer round, update the draft and call `validate_case` again. Continue
   in rounds of 2–3 only while material gaps remain. There is no fixed round limit.
   Never repeat a resolved question.
10. Stop asking when the important opportunities are exhausted or the contractor says
    no further data exists. Keep any remaining quality warnings visible without
    pressuring the contractor.
11. Show a concise final summary, validation findings, and `editor_url`.
12. Call `submit_case` only after the contractor makes an immediate, explicit decision
    to submit the reviewed version. The MCP server will additionally show a mandatory
    elicitation confirmation. A boolean tool argument or an earlier general request is
    not confirmation.

## Non-negotiable rules

- Never invent a client, metric, result, date, quote, scope, technology, or project
  characteristic.
- Ask when sources conflict; do not choose a convenient version.
- Propose structure and wording freely, but mark a forecast or target as such.
- Do not put local source content, local paths, full case text, upload URLs, or upload
  authorization tokens into logs.
- Manage only the authenticated contractor's own cases. Never attempt moderation,
  approval, rejection, administrative publication, or access to another contractor's
  case.
- `blocking_errors` must be resolved before submission. `quality_gaps` and
  `strengthening_opportunities` guide optional strengthening and do not justify invented
  facts.
