<!-- markdownlint-disable-file -->
# Implementation Details: Integrate visual-explainer into hve-core

## Context Reference

Sources: `.copilot-tracking/research/2026-03-02-visual-explainer-integration-research.md` (hve-core repo), `andrewDoing/hve-visual-explainer` source repository analysis, hve-core skill/prompt/collection conventions.

## Implementation Phase 1: Create skill directory structure

<!-- parallelizable: true -->

### Step 1.1: Create skill directory and subdirectories

Create the directory structure at `.github/skills/hve-core/visual-explainer/` in the hve-core repo:

```
.github/skills/hve-core/visual-explainer/
├── SKILL.md
├── LICENSE.txt
├── references/
│   ├── css-patterns.md
│   ├── libraries.md
│   ├── responsive-nav.md
│   └── slide-patterns.md
└── templates/
    ├── architecture.html
    ├── data-table.html
    ├── mermaid-flowchart.html
    └── slide-deck.html
```

Files:
* `.github/skills/hve-core/visual-explainer/` — New skill root directory
* `.github/skills/hve-core/visual-explainer/references/` — Reference materials subdirectory
* `.github/skills/hve-core/visual-explainer/templates/` — HTML template subdirectory

Success criteria:
* Directory structure exists with all subdirectories created

### Step 1.2: Copy and adapt SKILL.md with hve-core-compatible frontmatter

Copy `SKILL.md` from the source repo (`andrewDoing/hve-visual-explainer/SKILL.md`) to `.github/skills/hve-core/visual-explainer/SKILL.md` in hve-core. Update the frontmatter to match hve-core conventions.

**Source frontmatter:**
```yaml
---
name: visual-explainer
description: Generate beautiful, self-contained HTML pages that visually explain systems, code changes, plans, and data. Use when the user asks for a diagram, architecture overview, diff review, plan review, project recap, comparison table, or any visual explanation of technical concepts. Also use proactively when you are about to render a complex ASCII table (4+ rows or 3+ columns) — present it as a styled HTML page instead.
license: MIT
compatibility: Requires a browser to view generated HTML files. Optional surf-cli for AI image generation.
metadata:
  author: nicobailon
  version: "0.4.2"
---
```

**Target frontmatter (adapted):**
```yaml
---
name: visual-explainer
description: Generate beautiful, self-contained HTML pages that visually explain systems, code changes, plans, and data. Use when the user asks for a diagram, architecture overview, diff review, plan review, project recap, comparison table, or any visual explanation of technical concepts. Also use proactively when you are about to render a complex ASCII table (4+ rows or 3+ columns) — present it as a styled HTML page instead.
license: MIT
metadata:
  author: nicobailon
  version: "0.4.3"
---
```

Changes:
* Remove `compatibility` field (not part of hve-core skill spec; move this info into the SKILL.md body if not already there)
* Update `metadata.version` from `0.4.2` to `0.4.3` (matching package.json version)

Files:
* `andrewDoing/hve-visual-explainer/SKILL.md` — Source file (read)
* `.github/skills/hve-core/visual-explainer/SKILL.md` — Target file (create)

Success criteria:
* SKILL.md exists at the target location
* Frontmatter `name` matches directory name (`visual-explainer`)
* Frontmatter contains `name`, `description`, `license`, and `metadata` fields
* Body content is identical to source (no path changes needed — relative paths remain valid)

Context references:
* Research doc (Lines 96-108) — Frontmatter adaptation details

### Step 1.3: Copy all 4 reference files

Copy reference files from source to target without modification:

| Source | Target |
|---|---|
| `references/css-patterns.md` | `.github/skills/hve-core/visual-explainer/references/css-patterns.md` |
| `references/libraries.md` | `.github/skills/hve-core/visual-explainer/references/libraries.md` |
| `references/responsive-nav.md` | `.github/skills/hve-core/visual-explainer/references/responsive-nav.md` |
| `references/slide-patterns.md` | `.github/skills/hve-core/visual-explainer/references/slide-patterns.md` |

Files:
* `andrewDoing/hve-visual-explainer/references/*` — Source files (read)
* `.github/skills/hve-core/visual-explainer/references/*` — Target files (create)

Success criteria:
* All 4 reference files exist at the target location
* File contents are identical to source

### Step 1.4: Copy all 4 template files

Copy template files from source to target without modification:

| Source | Target |
|---|---|
| `templates/architecture.html` | `.github/skills/hve-core/visual-explainer/templates/architecture.html` |
| `templates/data-table.html` | `.github/skills/hve-core/visual-explainer/templates/data-table.html` |
| `templates/mermaid-flowchart.html` | `.github/skills/hve-core/visual-explainer/templates/mermaid-flowchart.html` |
| `templates/slide-deck.html` | `.github/skills/hve-core/visual-explainer/templates/slide-deck.html` |

Files:
* `andrewDoing/hve-visual-explainer/templates/*` — Source files (read)
* `.github/skills/hve-core/visual-explainer/templates/*` — Target files (create)

Success criteria:
* All 4 template files exist at the target location
* File contents are identical to source

### Step 1.5: Create LICENSE.txt

Copy the MIT license from the source repo's `LICENSE` file into `.github/skills/hve-core/visual-explainer/LICENSE.txt`. This follows the convention used by other hve-core skills (e.g., `web-artifacts-builder`, `pdf`).

Files:
* `andrewDoing/hve-visual-explainer/LICENSE` — Source file (read)
* `.github/skills/hve-core/visual-explainer/LICENSE.txt` — Target file (create)

Success criteria:
* `LICENSE.txt` exists in the skill directory
* Contains the MIT license text with original author attribution

## Implementation Phase 2: Create prompt files with viz- prefix

<!-- parallelizable: true -->

### Step 2.1: Create viz-diff-review.prompt.md

Create `.github/prompts/hve-core/viz-diff-review.prompt.md` from source `prompts/diff-review.md`.

Adapt frontmatter to hve-core conventions:
```yaml
---
description: "Generate a visual HTML diff review with before/after architecture diagrams, code analysis, and decision log"
---
```

Keep the body content intact. The prompt references "Load the visual-explainer skill" which works correctly since the skill name matches. Do not add an `agent` field — visual-explainer prompts are agent-agnostic (they work with any agent that has the skill loaded).

Files:
* `andrewDoing/hve-visual-explainer/prompts/diff-review.md` — Source (read)
* `.github/prompts/hve-core/viz-diff-review.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Body references to visual-explainer skill resolve correctly

Context references:
* Research doc (Lines 196-212) — Prompt naming rationale and mapping

### Step 2.2: Create viz-fact-check.prompt.md

Create `.github/prompts/hve-core/viz-fact-check.prompt.md` from source `prompts/fact-check.md`.

```yaml
---
description: "Verify factual accuracy of documents against the codebase using the visual-explainer skill"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/fact-check.md` — Source (read)
* `.github/prompts/hve-core/viz-fact-check.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Verification workflow references remain intact

### Step 2.3: Create viz-slides.prompt.md

Create `.github/prompts/hve-core/viz-slides.prompt.md` from source `prompts/generate-slides.md`.

```yaml
---
description: "Generate a magazine-quality HTML slide deck with distinctive aesthetics using the visual-explainer skill"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/generate-slides.md` — Source (read)
* `.github/prompts/hve-core/viz-slides.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Slide generation instructions remain intact

### Step 2.4: Create viz-plan.prompt.md

Create `.github/prompts/hve-core/viz-plan.prompt.md` from source `prompts/generate-visual-plan.md`.

```yaml
---
description: "Generate a visual implementation plan with state machines, API signatures, and edge case tables"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/generate-visual-plan.md` — Source (read)
* `.github/prompts/hve-core/viz-plan.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Visual plan generation workflow remains intact

### Step 2.5: Create viz-diagram.prompt.md

Create `.github/prompts/hve-core/viz-diagram.prompt.md` from source `prompts/generate-web-diagram.md`.

```yaml
---
description: "Generate a beautiful standalone HTML diagram with distinctive aesthetics using the visual-explainer skill"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/generate-web-diagram.md` — Source (read)
* `.github/prompts/hve-core/viz-diagram.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Diagram generation instructions remain intact

### Step 2.6: Create viz-plan-review.prompt.md

Create `.github/prompts/hve-core/viz-plan-review.prompt.md` from source `prompts/plan-review.md`.

```yaml
---
description: "Compare current codebase against a proposed plan with visual architecture diagrams and risk assessment"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/plan-review.md` — Source (read)
* `.github/prompts/hve-core/viz-plan-review.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Plan review workflow remains intact

### Step 2.7: Create viz-project-recap.prompt.md

Create `.github/prompts/hve-core/viz-project-recap.prompt.md` from source `prompts/project-recap.md`.

```yaml
---
description: "Rebuild mental model of project state with visual architecture snapshot, decision log, and cognitive debt hotspots"
---
```

Files:
* `andrewDoing/hve-visual-explainer/prompts/project-recap.md` — Source (read)
* `.github/prompts/hve-core/viz-project-recap.prompt.md` — Target (create)

Success criteria:
* Prompt file exists with correct frontmatter
* Project recap workflow and time-range parsing remain intact

## Implementation Phase 3: Update validation script

<!-- parallelizable: true -->

### Step 3.1: Add templates to recognized subdirectories

Edit `scripts/linting/Validate-SkillStructure.ps1` in the hve-core repo. Find the line:

```powershell
$script:RecognizedSubdirectories = @('scripts', 'references', 'assets', 'examples', 'tests')
```

Change it to:

```powershell
$script:RecognizedSubdirectories = @('scripts', 'references', 'assets', 'examples', 'tests', 'templates')
```

This single-line change allows skills to include a `templates/` subdirectory without triggering validation warnings.

Files:
* `scripts/linting/Validate-SkillStructure.ps1` — Modify (1 line change)

Success criteria:
* `templates` appears in the `$script:RecognizedSubdirectories` array
* No other changes to the validation script
* Existing skills continue to pass validation

## Implementation Phase 4: Update collection manifests

<!-- parallelizable: false -->

### Step 4.1: Add visual-explainer skill to hve-core.collection.yml

Edit `collections/hve-core.collection.yml` in the hve-core repo. Add the skill entry under the existing Skills section:

```yaml
  # Visual Explainer
  - path: .github/skills/hve-core/visual-explainer
    kind: skill
```

Place this after the existing skill entries (currently only `pr-reference`).

Files:
* `collections/hve-core.collection.yml` — Modify (add 3 lines)

Success criteria:
* Visual-explainer skill entry appears in the YAML
* Path matches the actual skill directory location
* `kind: skill` is specified

Context references:
* Research doc (Lines 129-153) — Collection manifest update details

Dependencies:
* Phase 1 completion (skill directory must exist)

### Step 4.2: Add viz-* prompt entries to hve-core.collection.yml

Add all 7 prompt entries to `collections/hve-core.collection.yml` under a new comment group:

```yaml
  # Visual Explainer Prompts
  - path: .github/prompts/hve-core/viz-diff-review.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-fact-check.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-slides.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-plan.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-diagram.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-plan-review.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-project-recap.prompt.md
    kind: prompt
```

Place this after the existing prompt entries in the Prompts section.

Files:
* `collections/hve-core.collection.yml` — Modify (add 16 lines)

Success criteria:
* All 7 prompt entries appear in the YAML
* Paths match actual prompt file locations
* All entries have `kind: prompt`

Dependencies:
* Phase 2 completion (prompt files must exist)

### Step 4.3: Add entries to hve-core-all.collection.yml

Add the same skill and prompt entries to `collections/hve-core-all.collection.yml` (the superset bundle). Place them in the appropriate sections that correspond to hve-core content.

```yaml
  # Visual Explainer
  - path: .github/skills/hve-core/visual-explainer
    kind: skill

  # Visual Explainer Prompts
  - path: .github/prompts/hve-core/viz-diff-review.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-fact-check.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-slides.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-plan.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-diagram.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-plan-review.prompt.md
    kind: prompt
  - path: .github/prompts/hve-core/viz-project-recap.prompt.md
    kind: prompt
```

Files:
* `collections/hve-core-all.collection.yml` — Modify (add 19 lines)

Success criteria:
* All entries from Step 4.1 and 4.2 also appear in the all-collection
* Placement is within the hve-core section of the superset bundle

Dependencies:
* Steps 4.1 and 4.2 completion

### Step 4.4: Update hve-core.collection.md documentation

Edit `collections/hve-core.collection.md` to document the new visual-explainer skill and the 7 viz-* prompts. Add a section describing:

* The visual-explainer skill and its purpose
* The 7 viz-* prompts and when to use each
* How visual-explainer complements existing text-based RPI workflow prompts

Files:
* `collections/hve-core.collection.md` — Modify (add documentation section)

Success criteria:
* Visual-explainer is documented in the collection description
* Each viz-* prompt is listed with its purpose
* Relationship to existing text-based prompts is explained

Dependencies:
* Steps 4.1-4.3 completion

## Implementation Phase 5: Validation

<!-- parallelizable: false -->

### Step 5.1: Run full project validation

Execute all validation commands in the hve-core repository:
* `npm run validate:skills` — Confirm skill structure passes (including `templates/` subdirectory)
* `npm run plugin:generate` — Regenerate plugin outputs with new collection entries
* `npm run plugin:validate` — Confirm collection metadata is consistent
* `npm run lint:md` — Validate all new and modified markdown files
* `npm run spell-check` — Catch unknown terms in new content

### Step 5.2: Fix minor validation issues

Iterate on validation failures:
* Add visual-explainer terminology to `.cspell` dictionary if needed (likely terms: mermaid, surfcli, flowchart, sparkline, nicobailon, surfing, Surfcli)
* Fix markdown lint errors (heading levels, line length, etc.)
* Resolve any plugin generation warnings

### Step 5.3: Report blocking issues

When validation failures require changes beyond minor fixes:
* Document the issues and affected files
* Provide the user with next steps
* Recommend additional research and planning rather than inline fixes
* Avoid large-scale refactoring within this phase

## Dependencies

* Node.js and npm (hve-core validation toolchain)
* PowerShell (Validate-SkillStructure.ps1)
* Both repositories accessible locally (`andrewDoing/hve-visual-explainer` and `hve-core`)

## Success Criteria

* `npm run validate:skills` passes with visual-explainer included
* `npm run plugin:generate` and `npm run plugin:validate` succeed
* `npm run lint:md` passes for all new files
* `npm run spell-check` passes (with dictionary additions as needed)
* All 7 `/viz-*` prompts are discoverable
* SKILL.md relative paths to `references/` and `templates/` resolve correctly
