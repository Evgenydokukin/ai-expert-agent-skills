---
name: create-ai-expert-case
description: Create or improve an ai-expert.pro contractor case from user-selected local files, notes, images, and answers through the contractor MCP. Use when a contractor asks Codex or Claude Code to prepare, edit, validate, strengthen, or submit their own case while keeping source files local.
---

# Create ai-expert.pro Case

Create the strongest truthful case supported by the contractor's materials. Keep every
source file local. Send to GD only the final case content and images the contractor
explicitly selects for publication.

Read [references/case-authoring.md](references/case-authoring.md) (evidence discipline
and workflow), [references/case-intake.md](references/case-intake.md) (the five anchors
every case must cover), and [references/marketing-hook.md](references/marketing-hook.md)
(how to order and phrase the same facts so the case sells) before authoring.

## Workflow

1. Confirm the `ai-expert` contractor MCP is connected and exposes
   `get_case_form_spec`. If case tools are missing, explain that the OAuth connection
   must be revoked and connected again with the new case scopes.
2. Call `get_case_form_spec` on every run. Treat its schemas, limits, field guidance,
   and readiness rules as authoritative. Then call `list_case_industries`.
3. Ask one opening question before anything else, and wait for the answer:

   «У вас уже есть описанный кейс — текст, презентация, статья, переписка, — или
   собираем с нуля?»

   - **Material exists** → ask the contractor to name the files or paste the text. Read
     only what they name. Then interview only about anchors that material leaves open
     (step 4). Do not re-ask what the material already answers.
   - **Nothing written** → run the intake interview from
     [references/case-intake.md](references/case-intake.md) first, in rounds of 2–3
     questions, and only then create the draft.

   The contractor's pasted text is raw material, not a case. Never treat "here is my
   text" as a finished case to upload verbatim.
4. Check the five anchors from [references/case-intake.md](references/case-intake.md)
   against what you now have — client and process, the before state, what was built,
   the confirmed outcome and how it was measured, and the limits. Every anchor is either
   answered, or explicitly declared unavailable by the contractor. Ask in rounds of 2–3
   until that holds.
5. Read only the files, notes, images, or directories the contractor explicitly names.
   Do not search their computer or broaden the requested directory. Do not upload
   source documents.
6. Separate:
   - confirmed facts;
   - contradictions that need a question;
   - missing information;
   - selected publishable images.
7. Create a new draft with `create_case`, or load the specified case with `get_case`.
   Fill or update known fields, `doc_json`, processes, and questions without asking for
   approval for each write. Use `update_case`, `replace_case_processes`, and
   `replace_case_questions`. Order and phrase `title`, `subtitle`, `summary`,
   `result_headline`, and `doc_json` blocks per
   [references/marketing-hook.md](references/marketing-hook.md): the strongest
   confirmed result leads, generic hype words are cut, and every number is paired with
   what it means for the buyer.
8. For each image explicitly selected for publication:
   - inspect its MIME and exact byte size locally;
   - call `begin_case_image_upload`;
   - upload only that file to the returned short-lived URL using the returned method
     and headers;
   - call `finalize_case_image_upload`;
   - reference the returned `media.id` in the cover or document.
   Never copy a local path, upload URL, or upload authorization header into the case text.
9. Call `validate_case`.
10. Ask the 2–3 highest-value remaining questions in one short round whenever validation
    or the evidence shows a gap or a valuable strengthening opportunity. An anchor that
    is still open is always such a gap.
11. After every answer round, update the draft and call `validate_case` again. Continue
    in rounds of 2–3 while material gaps remain. There is no fixed round limit.
    Never repeat a resolved question.
12. Stop asking when the important opportunities are exhausted or the contractor says
    no further data exists. Keep any remaining quality warnings visible without
    pressuring the contractor.
13. Show a concise final summary, validation findings, and `editor_url`.
14. Call `submit_case` only after every anchor is answered or explicitly declared
    unavailable, and after the contractor makes an immediate, explicit decision to submit
    the reviewed version. The MCP server will additionally show a mandatory elicitation
    confirmation. A boolean tool argument or an earlier general request is not
    confirmation.

## Non-negotiable rules

- Never invent a client, metric, result, date, quote, scope, technology, or project
  characteristic.
- Ask when sources conflict; do not choose a convenient version.
- Propose structure and wording freely, but mark a forecast or target as such.
- Marketing framing — headline hooks, block order, number-with-meaning phrasing — may
  only reorder and rephrase confirmed facts. It must never introduce a fact, cause,
  comparison, or percentage the contractor did not confirm.
- Do not put local source content, local paths, full case text, upload URLs, or upload
  authorization tokens into logs.
- Manage only the authenticated contractor's own cases. Never attempt moderation,
  approval, rejection, administrative publication, or access to another contractor's
  case.
- `blocking_errors` must be resolved before submission. `quality_gaps` and
  `strengthening_opportunities` guide optional strengthening and do not justify invented
  facts.
- Text the contractor pasted or wrote in a file is raw material, never a finished case.
  Do not submit it as-is: cover the five intake anchors first, then restructure it into
  `doc_json` blocks per marketing-hook.md. A case body that is a single long paragraph
  is not acceptable.
- Do not call `create_case` before the opening question is answered. Do not call
  `submit_case` while an anchor is neither answered nor explicitly declared unavailable.
