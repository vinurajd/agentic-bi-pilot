# BUILD-AUDIT — Agentic BI Pilot plugin

Built 2026-11-19 (America/Chicago), at Vinuraj's direction after a brainstorm round. Package: `~/workspace/agentic-bi-plugin/`. Three skill folders also installed to `~/workspace/custom-skills/`. Nothing published; repository creation and release are Vinuraj's launch steps, on his word.

## What was built
- Plugin manifests (`.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, root `marketplace.json`), name `agentic-bi-pilot`, version 1.0.0, marketplace `vinurajd-skills` — the family layout used by PremedPilot and the Contract Checker packages. All three JSON files parse.
- Three skills, each self-contained (SKILL.md + FAQ.md with the `--help` behaviour + one reference file):
  - `agentic-bi-design-advisor` — references/architecture-taxonomy.md
  - `agentic-bi-evaluation-planner` — references/evaluation-framework.md
  - `agentic-bi-deployment-readiness` — references/deployment-checklist.md
- README.md (install paths for Claude Code plugin and folder installs; honesty notes), LICENSE (MIT, copied from the checker package).

## Source discipline
- All substance distilled from the paper's own section files in `~/workspace/goals/eb-1a-petition-preparation/files/survey-paper-ai-agents-ba/` (sections 2, 3, 6, 7), read in full during this build. No figure, exemplar, or claim was added beyond those files; spot figures carried with citations: Data Interpreter 94.9% InfiAgent-DABench; SELA 65–80%; AIDE MLE-bench 4×; Spider 2.0 ~21%; DABStep 14.55%; MAST 14 modes / 3 categories / 41–86.7%; ToolEmu 23.9%; PrivacyLens 90–95% vs 25–40%; FrugalGPT up to 98%; RouteLLM 2×+; Rahman et al. >90%.
- Citation, per Vinuraj's direction: the framework is cited everywhere exactly as "under review at IEEE IT Professional." The preprint DOI is not used.
- Both personas (analytics leader; practitioner) are served in every skill's intake, workflow, and deliverable shape, per his decision.
- Contract Checker composition is by reference and recommendation, not by bundled MCP auto-start: the checker is unpublished, so an auto-start server declaration would break on install. The readiness skill records whether the checker audit has run and carries its findings into Area 6.

## Cold tests (test-runs/)
- A, Evaluation Planner, practitioner (wrong revenue numbers in production): PASS on all five hard-rule checks recorded in the file.
- B, Design Advisor, leader (two use-case classes, two different patterns recommended): PASS on all five checks.
- C, Deployment Readiness, practitioner (spreadsheet/email ingestion, prompt-level access control): PASS on all six checks; overall verdict Do not ship, following the blocking areas.
- Tests are simulated consultations run against the SKILL.md workflows by the builder, as with the PremedPilot cold tests; they are not independent-user tests.

## Lessons comparison (AGENTS.md + standing self-review checklist, item by item)
- Understand before concluding: the build waited for the brainstorm and his two decisions (personas, citation) before any file was written. CHECKED.
- Verify against the primary source: the paper's own sections are the source and were read in full this session; no venue or pricing fact is asserted in the package. CHECKED.
- Exact-instruction rule: personas = both, citation = under review at IEEE IT Professional, exactly as directed. CHECKED.
- No version language in file or folder names: package and skill names carry none; the version lives only in plugin.json, as in the family packages. CHECKED.
- One canonical deliverable per document: the package is the single canonical tree; the custom-skills copies are installs of it, as with the earlier skills. CHECKED.
- Never edit sources with sed: all files written whole with the write tool. CHECKED.
- Nearest-neighbour census: the neighbouring artefacts are the Contract Checker (semantic layer) and PremedPilot; differentiation is written into the README and the readiness skill (agent-level vs layer-level audit). CHECKED.
- AI disclosure: not applicable to a skill package; the README's honesty notes carry the paper-status disclosure instead. CHECKED.
- Rendered-output inspection: JSON validated by parse; file tree listed and read back; installed copies verified by listing and head read. No PDF deliverable in this build. CHECKED.

## Known limitations
- `claude plugin validate` could not be run (no Claude CLI on this VM); structural validity rests on JSON parsing and conformance to the two family packages that predate it. The Anthropic portal's Validate step, when the plugin is submitted, runs stricter checks.
- Publication sequence is unsettled: the checker launch is sequenced after the NTCS resubmission; this plugin's launch order relative to it is Vinuraj's call.
