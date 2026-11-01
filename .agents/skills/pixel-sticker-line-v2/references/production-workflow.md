# Reusable LINE Sticker Production Workflow

Use this reference with `pixel-sticker-line-v2` for any character or chat intent.
Keep character identity, art style, actions, and export settings as project data.
This workflow covers LINE stickers; other platforms need their own product rules.

## Entry and approval rules

- New set: start at 00. Existing set: inspect available files and resume at the
  earliest affected step. Do not recreate valid work merely to populate folders.
- Choose the exact LINE product before canvas, quantity, or animation decisions.
  Read `line-creators-market.md`; for products outside its coverage, consult the
  exact official guide before production. Store the source and verification date.
- Resolve missing information that changes the deliverable; use stated assumptions
  for routine choices. Do not require every optional template field to be filled.
- Default gates are 01, 02, 04, and 07. At each pending gate, finish the scoped work,
  provide viewable artifacts and checks, then wait before dependent production.
  Independent inspection and planning may continue. Existing user approval or an
  explicit continuous-work instruction can cover multiple gates; record its scope.
- Approval attaches to an artifact revision. A design/spec change outside the
  approved scope reopens the affected gate and invalidates dependent outputs.
  Routine corrections within the approved design do not require repeated approval.
- At each completed stage, record input revisions, work performed, output paths,
  validation result, and next step in `production_state.yaml`. Keep user updates
  concise. Distinguish `draft`, `validated`, and `approved`; passing QA alone does
  not imply user approval.
- If tools cannot create or inspect a required file, report the missing capability
  and affected stage. Never claim file creation, playback, or approval without evidence.

## Steps 00–08: input / process / output

| Step | Input | Process and validation | Output | Gate |
|---|---|---|---|---|
| 00 Configuration | Request, references, existing assets | Select product, quantity, chat intents, output scope, tooling, and approval mode; establish feasible canvas and export constraints | `config/project_config.yaml`, `config/production_state.yaml` | Resolve deliverable-critical gaps |
| 01 Character sheet | Reference images or description | Inspect or create identity sheet: silhouette, proportions, identifying features, colors, useful views, expressions; avoid unnecessary views | `character/character_sheet.png` or validated existing sheet | Approve character |
| 02 Sprite specification | Accepted character sheet | Define logical grid, integer enlargement, output canvases, palette, outline, shading/light, perspective, anchor, text rules; prove fit with a master sprite | `sprite/sprite_spec.yaml`, `sprite/master_sprite.png` | Approve spec and master |
| 03 Action planning | Spec and chat-intent list | Assign a stable ID to each sticker; define message, expression, gesture and composition. For animation, plan key poses, frame order, per-frame delays, cycle duration, and finite loops within product limits | `stickers/{id}/plan.yaml` | — |
| 04 Key poses | Master and sticker plan | Draw readable extremes and breakdowns; check identity, silhouette, text, and full movement bounds. For static stickers, create the pose draft | `stickers/{id}/keyposes.png` | Approve poses, per sticker or agreed batch |
| 05 Production | Accepted poses and spec | Draw final static art or animation frames; preserve pixel clusters, palette, anchor, and frame canvas; inspect at 1x | `stickers/{id}/art.png` or `frames/frame_###.png` | — |
| 06 Assembly | Art/frames and timing | For animation, assemble sheet, explicit timing/order metadata, and playable preview. Static sets need a contact sheet only when useful | `spritesheet.png`, `timing.yaml`, `preview.apng` under each animated sticker | — |
| 07 QA | Assets, references, spec | Review pixel quality, character fidelity, chat readability and product compliance separately; repair affected stages and recheck | `qa/qa_report.md` and corrected assets | Approve reviewed assets |
| 08 Export | Accepted assets and exact product requirements | Export all required sticker, main and thumbnail images, metadata, and optional ZIP; decode/inspect final files again | `export/line/` and file manifest | Deliver files and remaining issues |

For static sets, animation planning fields, frame production, timing, loops, APNG
and sprite sheets are not applicable. Do not manufacture animation artifacts.
For an animation, keep plan, key poses, frames, timing and preview separate per ID.
A sheet is an intermediate production asset, not a LINE submission sticker.

## Configuration templates

Adapt these YAML examples to the task; `null` means unresolved or not applicable.
Populate product constraints from the selected official guide rather than treating
example values as official limits. Never treat this template as a completed project.

`config/project_config.yaml`:

```yaml
schema_version: 1
project_name: null
character:
  reference_paths: []
  description: null
  existing_sheet: null
  identity_features: []
product:
  platform: LINE
  type: null # static, animated, or the exact other LINE product
  sticker_count: null
  official_guide_url: null
  verified_on: null
  verification_status: pending # verified or unavailable
  constraints: {} # canvases, quantity, color mode, file sizes, timing, etc.
art:
  style: pixel_art
  native_grid_px: null # [width, height]
  integer_scale: null
  sticker_canvas_px: null
  main_canvas_px: null
  thumbnail_canvas_px: null
  palette: [] # hex colors; finalize in sprite_spec.yaml
  outline_policy: null
  text_language: null
approval:
  mode: staged # continuous only when authorized by the user
  gates: [character_sheet, sprite_spec, keyposes, qa]
  authorization_scope: null
stickers: [] # each: id, intent, phrase, action; details in its plan.yaml
deliverables:
  editable_source: null # only when requested and supported
  submission_images: true
  zip: false
```

`sprite/sprite_spec.yaml` should record the sheet revision, master path, native
grid, integer scale, output canvases, palette roles, outline width at native size,
light source, shading/cluster policy, perspective, proportions, anchor, text
treatment, and identity features that must persist. Plan main and thumbnail
compositions separately when their dimensions cannot use the master unchanged.

`stickers/{id}/plan.yaml`, animated example:

```yaml
id: greeting
intent: greeting
phrase: null
action: wave
spec_revision: null
key_poses: [readable_greeting, hand_out, hand_in, settle]
animation:
  frame_order: [] # ordered paths; populate after production
  frame_delays_ms: [] # one positive duration per entry in frame_order
  cycle_duration_ms: null # sum of frame delays; validate against product rules
  loop_count: null # finite; validate cycle duration multiplied by loops
  loop_behavior: return_to_start
  first_frame_intent: readable_greeting
  anchor_px: null
  canvas_px: null
```

Use `animation: null` for a static sticker. The key-pose count is a creative
choice; encoded APNG frame count must independently satisfy the product rules.

`config/production_state.yaml` minimal record:

```yaml
current_step: '00'
artifacts: [] # path, revision, input_revisions, status
stages: [] # step, input_revisions, process, output_paths, validation, next_step
approvals: [] # gate, artifact_revisions, user_instruction, scope
pending_gate: null
invalidated_outputs: []
```

## Production invariants

- Use deliberate frame-by-frame pixel drawing. Squash/stretch or rotation describes
  the pose; redraw and clean pixels instead of preserving blurred transformed art.
  Integer translations and controlled reuse of unchanged clusters are appropriate.
- Maintain one native pixel scale and consistent construction rules across the set.
  Fit motion and text inside the allowed bounds before full production; avoid
  non-integer resizing as a last-minute export fix.
- Keep source frames on a shared canvas and anchor. Trim the union of motion bounds
  consistently across the animation, rather than independently recentering frames.
  Validate decoded/composited APNG frames even when the encoder uses delta rectangles.
- Record exact playback order and positive per-frame delays. Check their sum and
  loop count against the official product limits. Check encoded frame count after
  optimization, since repeated frames may merge. Do not pad an invalid animation
  with identical frames and assume it is compliant.
- Make the first encoded frame communicate the sticker's intended message as a still.
  Recheck the loop seam after changing that frame or rearranging the sequence.
- A preview may use `.apng`; LINE submission APNGs use the extension specified in
  `line-creators-market.md`. Renaming an extension does not convert image encoding.

## QA and export evidence

Read `sharp_edges.md` and `validations.md` for pixel quality, and
`line-creators-market.md` for submission checks. These are distinct reviews.

Check character features, proportions, palette/outline consistency, stray pixels,
halos, frame alignment, unintended shimmer, text spelling, and readability at 1x on
light and dark backgrounds. For animation, inspect actual playback, key-pose
timing, loop seam, and the first-frame still. Document checks that could not run.

Inspect final exported files, not only plans: actual encoding, decoded dimensions,
color mode, transparency, file sizes, required quantities, and all main/thumbnail
assets. For APNG also inspect effective frames, delays, finite loops, compositing
and total playback. Recheck ZIP size and contents when a ZIP is requested.

In `qa/qa_report.md`, separate hard submission blockers, likely review risks, and
optional improvements. Include measured evidence, visual findings, verification
limitations, affected file paths, and repair status. In the export manifest, map
each stable sticker ID to its final filename and include each file's role and
measured checks. Never guarantee LINE review approval. Export does not authorize
uploading, publishing, or sending files externally.

## Project layout and reuse

```text
project/
  config/{project_config.yaml,production_state.yaml}
  character/references/
  character/character_sheet.png
  sprite/{sprite_spec.yaml,master_sprite.png}
  stickers/{id}/plan.yaml
  stickers/{id}/keyposes.png
  stickers/{id}/art.png                 # static
  stickers/{id}/frames/frame_###.png    # animated
  stickers/{id}/{spritesheet.png,timing.yaml,preview.apng} # animated
  qa/qa_report.md
  export/line/                          # required images, manifest, optional ZIP
```

Use an existing project layout if it provides equivalent traceability.

- New character: update 00, restart 01, and invalidate old character-dependent work.
- Additional action: reuse the accepted sheet/spec; update set quantity and intent
  variety in 00, then start the new sticker at 03 and rerun set-level QA/export.
- Timing-only change: revisit 03/06, then QA/export; redraw only if motion needs it.
- QA failure: return to the earliest responsible step and rebuild affected outputs.
- Product/platform change: check new constraints at 00 before assuming asset reuse.
  Re-export at 08 only if existing artwork fits; revisit spec/production otherwise.
  For non-LINE work, hand off to an appropriate skill with the reusable source assets.

## Reusable execution prompt

> Use $pixel-sticker-line-v2 to create or extend a LINE pixel-art sticker set from
> the supplied character reference. Read its production workflow and applicable
> references. Start at project configuration or resume from valid existing assets.
> Record product, chat intents, style, grid, palette, actions, and output settings
> as project data. Follow steps 00–08 only where relevant, with staged approval at
> the character sheet, master/specification, key poses, and QA unless I have
> authorized continuous work. Present actual artifacts at each pending gate.
> Preserve character identity and crisp pixels, repair affected stages when QA
> fails, and validate the final LINE submission files. Report missing capabilities
> and unverified checks clearly; do not claim files or approvals that do not exist.
