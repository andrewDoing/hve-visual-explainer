---
applyTo: '.copilot-tracking/changes/20260302-visual-explainer-hve-core-integration-changes.md'
---
<!-- markdownlint-disable-file -->
# Implementation Plan: Integrate visual-explainer into hve-core

## Overview

Integrate the `visual-explainer` skill and its 7 prompts into the `hve-core` monorepo as a first-class skill under the `hve-core` collection, following all established hve-core conventions for skill structure, prompt naming, collection manifests, and validation.

Follow all instructions from the hve-core repository's `.github/copilot-instructions.md`.

## Objectives

* Add `visual-explainer` as a validated skill at `.github/skills/hve-core/visual-explainer/` in the hve-core repo
* Create 7 `viz-*` prefixed prompt files in `.github/prompts/hve-core/`
* Update `Validate-SkillStructure.ps1` to recognize `templates` as a valid subdirectory
* Register the skill and all prompts in both `hve-core.collection.yml` and `hve-core-all.collection.yml`
* Pass all hve-core validation (`validate:skills`, `plugin:generate`, `plugin:validate`, `lint:md`, `spell-check`)

## Context Summary

### Project Files

* `SKILL.md` — Core skill instructions (409 lines): workflow rules, diagram types, aesthetics, anti-patterns
* `references/` — 4 reference files (3,891 lines): css-patterns.md, libraries.md, responsive-nav.md, slide-patterns.md
* `templates/` — 4 HTML templates (2,484 lines): architecture.html, data-table.html, mermaid-flowchart.html, slide-deck.html
* `prompts/` — 7 prompt files (413 lines): diff-review, fact-check, generate-slides, generate-visual-plan, generate-web-diagram, plan-review, project-recap
* `LICENSE` — MIT license file

### References

* `.copilot-tracking/research/2026-03-02-visual-explainer-integration-research.md` (in hve-core repo) — Full integration research with overlap analysis, naming decisions, and structural mapping
* hve-core `.github/skills/shared/pr-reference/` — Example skill structure with SKILL.md, references/, scripts/, tests/
* hve-core `collections/hve-core.collection.yml` — Target collection manifest
* hve-core `scripts/linting/Validate-SkillStructure.ps1` — Skill validation script (recognized subdirs: scripts, references, assets, examples, tests)

### Standards References

* hve-core `.github/copilot-instructions.md` — Repository conventions and coding standards

## Implementation Checklist

### [ ] Implementation Phase 1: Create skill directory structure

<!-- parallelizable: true -->

* [ ] Step 1.1: Create the skill directory at `.github/skills/hve-core/visual-explainer/` with `references/` and `templates/` subdirectories
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 13-32)
* [ ] Step 1.2: Copy and adapt SKILL.md with hve-core-compatible frontmatter
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 34-62)
* [ ] Step 1.3: Copy all 4 reference files into `references/`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 64-82)
* [ ] Step 1.4: Copy all 4 template files into `templates/`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 84-102)
* [ ] Step 1.5: Create LICENSE.txt in the skill directory
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 104-117)

### [ ] Implementation Phase 2: Create prompt files with viz- prefix

<!-- parallelizable: true -->

* [ ] Step 2.1: Create `viz-diff-review.prompt.md` in `.github/prompts/hve-core/`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 123-145)
* [ ] Step 2.2: Create `viz-fact-check.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 147-162)
* [ ] Step 2.3: Create `viz-slides.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 164-179)
* [ ] Step 2.4: Create `viz-plan.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 181-196)
* [ ] Step 2.5: Create `viz-diagram.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 198-213)
* [ ] Step 2.6: Create `viz-plan-review.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 215-230)
* [ ] Step 2.7: Create `viz-project-recap.prompt.md`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 232-247)

### [ ] Implementation Phase 3: Update validation script

<!-- parallelizable: true -->

* [ ] Step 3.1: Add `templates` to `$script:RecognizedSubdirectories` array in `Validate-SkillStructure.ps1`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 253-271)

### [ ] Implementation Phase 4: Update collection manifests

<!-- parallelizable: false -->

* [ ] Step 4.1: Add visual-explainer skill entry to `hve-core.collection.yml`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 277-310)
* [ ] Step 4.2: Add all 7 viz-* prompt entries to `hve-core.collection.yml`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 312-346)
* [ ] Step 4.3: Add visual-explainer skill and prompts to `hve-core-all.collection.yml`
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 348-368)
* [ ] Step 4.4: Update `hve-core.collection.md` to document the visual-explainer skill and prompts
  * Details: .copilot-tracking/details/20260302-visual-explainer-hve-core-integration-details.md (Lines 370-390)

### [ ] Implementation Phase 5: Validation

<!-- parallelizable: false -->

* [ ] Step 5.1: Run full project validation
  * Execute `npm run validate:skills` to confirm skill structure passes
  * Execute `npm run plugin:generate` to regenerate plugin outputs
  * Execute `npm run plugin:validate` to confirm collection metadata
  * Execute `npm run lint:md` to validate markdown
  * Execute `npm run spell-check` to catch unknown terms
* [ ] Step 5.2: Fix minor validation issues
  * Add visual-explainer terminology to `.cspell` dictionary (e.g., mermaid, surfcli, flowchart, sparkline, nicobailon)
  * Iterate on lint errors and build warnings
  * Apply fixes directly when corrections are straightforward
* [ ] Step 5.3: Report blocking issues
  * Document issues requiring additional research
  * Provide user with next steps and recommended planning
  * Avoid large-scale fixes within this phase

## Dependencies

* Node.js and npm (for hve-core validation scripts)
* PowerShell (for `Validate-SkillStructure.ps1`)
* Access to both `andrewDoing/hve-visual-explainer` (source) and `hve-core` (target) repositories
* hve-core development environment with all validation tooling configured

## Success Criteria

* `visual-explainer` skill directory passes `npm run validate:skills`
* All 7 `viz-*` prompts are registered and discoverable via `/viz-` tab completion
* Both `hve-core.collection.yml` and `hve-core-all.collection.yml` include the new entries
* `npm run plugin:generate` and `npm run plugin:validate` succeed
* `npm run lint:md` passes for all new markdown files
* `npm run spell-check` passes with any necessary dictionary additions
* All relative paths in SKILL.md (to references/ and templates/) resolve correctly from the new location
