---
agent: 'task-implementor'
---

<!-- markdownlint-disable-file -->
# Implementation Prompt: Integrate visual-explainer into hve-core

## Implementation Instructions

### Step 1: Create Changes Tracking File

Create `20260302-visual-explainer-hve-core-integration-changes.md` in `.copilot-tracking/changes/` if it does not exist.

### Step 2: Execute Implementation

Follow the hve-core repository's `.github/copilot-instructions.md` and systematically implement #file:../plans/20260302-visual-explainer-hve-core-integration-plan.instructions.md step-by-step. Reference #file:../details/20260302-visual-explainer-hve-core-integration-details.md for detailed specifications at each step. Follow all project standards and conventions.

**Important context:**
- Source repository: `andrewDoing/hve-visual-explainer` (files to copy from)
- Target repository: `hve-core` (where changes are applied)
- All file copy operations go from source → target with adaptations noted in details
- The `templates/` subdirectory requires a validation script update (Phase 3) to be recognized
- Use `viz-` prefix for all prompt files to differentiate from existing text-based workflow prompts
- Do NOT copy `package.json` or `banner.png` from source — these are not used by hve-core

When ${input:phaseStop:true} is true, stop after each Phase for user review.
When ${input:stepStop:false} is true, stop after each Step for user review.

### Step 3: Cleanup

When all phases are checked off (`[x]`) and completed:

1. Provide a markdown link and summary of all changes from #file:../changes/20260302-visual-explainer-hve-core-integration-changes.md to the user. Keep the summary brief, add spacing around lists, and wrap file references in markdown links.
2. Provide markdown links to the plan, details, and research documents. Recommend cleaning these files up.
3. Delete .copilot-tracking/prompts/implement-visual-explainer-hve-core-integration.prompt.md

## Success Criteria

* [ ] Changes tracking file created
* [ ] All plan items implemented with working code
* [ ] All detailed specifications satisfied
* [ ] Project conventions followed
* [ ] Changes file updated continuously
* [ ] `npm run validate:skills` passes
* [ ] `npm run plugin:generate` and `npm run plugin:validate` succeed
* [ ] `npm run lint:md` passes
* [ ] `npm run spell-check` passes
