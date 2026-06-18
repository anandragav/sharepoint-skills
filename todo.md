# Skills README Quality Check — Findings & Tracking

Quality review of every skill folder under [`Skills/`](./Skills/) for README completeness and consistency.

**Status: ✅ All findings resolved.** All 30 skills are now fully compliant and aligned to the standard format.

Checks performed per skill:

1. **Preview picture** — README references an image (`![preview](./assets/preview.png)`) that illustrates the skill.
2. **Visitor-stats tracking image** — hidden `<img src="https://m365-visitor-stats.azurewebsites.net/sharepoint-skills/skills/<skill>" />` at the end of the README.
3. **Consistency** — credit table heading/format, `## Version history`, and `## Disclaimer` sections present and consistent.

## Summary status matrix (after fixes)

| Skill | Preview img in README | Visitor-stats img | Version history | Disclaimer | Credit heading |
|---|:---:|:---:|:---:|:---:|---|
| dossier | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| exec-report | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| file-classifier | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| invoice-po-reconciliation | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| kb-ai-review-lite | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| library-cleanup | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| list-styling | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| organize-library | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rename-files-date-prefix | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| review-council | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-compliance-review | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-content-finder | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-content-generation | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-extraction | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-proposal-review | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-quality-tone-review | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| rfp-response-strategy-synthesis | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| roadmap-timeline | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| scorecard-matrix | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| site-storage-heatmap | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-bento | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-blueprint | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-figma-clean | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-glassmorphism | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-high-contrast | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-monochrome | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-neobrutalism | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-pastel | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-retro | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |
| style-terminal | ✅ | ✅ | ✅ | ✅ | SharePoint Skill |

**30 of 30 skills are fully compliant.** All previously identified issues in the 7 `rfp-response-*` skills and `kb-ai-review-lite` have been fixed.

---

## Completed tasks

### 1. Added missing preview image to README ✅

- [x] [rfp-response-compliance-review/README.md](./Skills/rfp-response-compliance-review/README.md)
- [x] [rfp-response-content-finder/README.md](./Skills/rfp-response-content-finder/README.md)
- [x] [rfp-response-content-generation/README.md](./Skills/rfp-response-content-generation/README.md)
- [x] [rfp-response-extraction/README.md](./Skills/rfp-response-extraction/README.md)
- [x] [rfp-response-proposal-review/README.md](./Skills/rfp-response-proposal-review/README.md)
- [x] [rfp-response-quality-tone-review/README.md](./Skills/rfp-response-quality-tone-review/README.md)
- [x] [rfp-response-strategy-synthesis/README.md](./Skills/rfp-response-strategy-synthesis/README.md)

> Follow-up: confirm each `assets/preview.png` is an actual screenshot of the skill output (not a placeholder/logo) per the repo pre-submission checklist.

### 2. Added missing visitor-stats tracking image ✅

- [x] [kb-ai-review-lite/README.md](./Skills/kb-ai-review-lite/README.md)
- [x] All 7 `rfp-response-*` READMEs

### 3. Added missing `## Version history` section ✅

- [x] All 7 `rfp-response-*` READMEs — `1.0 | June 2026 | Initial Release`

### 4. Added missing `## Disclaimer` section ✅

- [x] All 7 `rfp-response-*` READMEs — standard single-line text

### 5. Consistency — credit table heading/format ✅

- [x] Standardized on `## SharePoint Skill` with a `| Solution | Author(s) |` table.
- [x] Converted the 8 outliers (`kb-ai-review-lite` + all 7 `rfp-response-*` skills) from `## Contribution` (Property/Value).
- [x] Updated the template in [Skills/README.md](./Skills/README.md) to the full standard layout (preview image, `SharePoint Skill` table, `Version history`, `Disclaimer`, visitor-stats image), plus the Required-files table and pre-submission checklist wording.

### 6. Consistency — minor wording ✅

- [x] [kb-ai-review-lite/README.md](./Skills/kb-ai-review-lite/README.md) — `Initial release` → `Initial Release`; collapsed the multi-line disclaimer to the single-line standard.

---

## Verification notes

- Every skill has a `preview.png` under `assets/` (30/30 confirmed) and now references it in the README.
- Visitor-stats image present in all 30 skill READMEs (verified via search).
- No remaining `## Contribution` headings or lowercase `Initial release` entries in skill READMEs (verified via search).
- Content accuracy (skill description vs. SKILL.md behavior) was spot-checked at the README level only; a deeper SKILL.md-vs-README cross-check remains an optional follow-up.

---

# sample.json Quality Check — Findings & Tracking

Validation of every skill's [`assets/sample.json`](./Skills/) (the PnP samples-gallery metadata). **No changes applied yet — these are findings only.**

Checks performed per skill (all 30, programmatically):

- JSON is syntactically valid.
- `name` equals `pnp-sharepoint-skills-<folder>`.
- `url` points to `.../Skills/<folder>` and `thumbnails[0].url` points to `.../Skills/<folder>/assets/preview.png`.
- `authors[0]` — `gitHubAccount` is a real handle (not a placeholder), `pictureUrl` matches `https://github.com/<handle>.png`, and `name` is present.
- `products`, `metadata` (`SAMPLE-TYPE`, `SKILL-CATEGORY`), `creationDateTime`/`updateDateTime` present and well-formed.
- `references` includes the agentskills.io specification (repo norm).

**Result: all 30 sample.json files are now fully valid and consistent.** Both items below have been fixed.

## Tasks

### A. Fix placeholder author — `kb-ai-review-lite` ✅

[Skills/kb-ai-review-lite/assets/sample.json](./Skills/kb-ai-review-lite/assets/sample.json) had a leftover template author block. Fixed to match the README credit (`GeorgiaGit`).

- [x] `"gitHubAccount": "your-handle"` → `"GeorgiaGit"`
- [x] `"pictureUrl": "https://github.com/your-handle.png"` → `"https://github.com/GeorgiaGit.png"`

### B. Consistency — added agentskills.io spec reference to the 10 style skills ✅

All 10 `style-*` skills now include the standard agentskills.io specification entry under `references` (added as the first entry, before the existing "List Styling Engine" and "Demo video" references).

- [x] style-bento
- [x] style-blueprint
- [x] style-figma-clean
- [x] style-glassmorphism
- [x] style-high-contrast
- [x] style-monochrome
- [x] style-neobrutalism
- [x] style-pastel
- [x] style-retro
- [x] style-terminal

> Note: the `style-*` skills' `references` link to the `list-styling` skill ("List Styling Engine") is **intentional and correct** and was preserved.

## sample.json verification notes

- All 30 files are valid JSON (parsed successfully, re-verified after edits).
- `name` / `url` / `thumbnails[0].url` paths match each skill folder for all 30.
- `pictureUrl` matches `gitHubAccount` for all 30 skills (kb-ai-review-lite fixed).
- Author handles match the README credit tables: `zrosenfield` (Zach Rosenfield), `JoeFranc` (Joe Komban), `LeonArmston` (Leon Armston), `mattwolodarsky-droid` (Matt Wolodarsky), `GeorgiaGit` (Andrew Burns).
- Every file has `products`, a `SKILL-CATEGORY`, and the agentskills.io specification reference; `creationDateTime`/`updateDateTime` are valid ISO dates consistent with the README version-history months.
- Author GitHub handles and picture URLs were validated for format/consistency, not by fetching each profile online — a live 200-check is an optional extra step if desired.
