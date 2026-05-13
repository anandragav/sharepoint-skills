# Skills

AI skills are instruction files that give a Copilot agent a focused capability. Each skill lives in its own folder and is installed by uploading that folder to the **Skills** library in SharePoint.

Some skills also include a `demo/` subfolder containing sample content you can use to try the skill end-to-end (e.g., [`libraries/library-cleanup/demo/`](./libraries/library-cleanup/demo/)). When uploading a skill folder to SharePoint, simply skip the `demo/` subfolder — only `SKILL.md` is required for the skill to run.

## Quick links

- **Browse skills:** [Libraries](#libraries) · [Operations](#operations)
- **Install:** [Installing a Skill](#installing-a-skill)
- **Contribute:** [Creating a Skill](#creating-a-skill) · [Categories](#categories) · [Required files](#required-files) · [File templates](#file-templates) · [✅ Pre-submission checklist](#pre-submission-checklist)

---

## Libraries

| Folder | Skill | Description |
|---|---|---|
| [file-classifier/](./libraries/file-classifier/) | File Classifier | Classifies files in a SharePoint document library by reading their content and matching them to known content types (Contracts, Invoices, Purchase Orders). Creates the appropriate metadata columns, extracts values from each file, and saves them automatically. Use when asked to classify, tag, or extract metadata from documents in a library. |
| [library-cleanup/](./libraries/library-cleanup/) | Library Cleanup | Organizes a document library by scanning for duplicates, bad file names, empty folders, and excessive nesting. Reads file content to generate meaningful rename suggestions, presents a visual before/after comparison with an Organization Score, then executes the full cleanup with a live TODO checklist the user can follow along with. Triggered when someone says "clean up file demo". |
| [organize-library/](./libraries/organize-library/) | Organize Library | Fully organizes a SharePoint document library end-to-end: classifies files by content type, applies brand-consistent column formatting (pills, data bars, overdue highlights), creates filtered views per content type, colors folders, and sets up notification rules for overdue items. Orchestrates the file-classifier skill and reads SHAREPOINT.md for brand colors. |

## Operations

| Folder | Skill | Description |
|---|---|---|
| [site-storage-heatmap/](./operations/site-storage-heatmap/) | Site Storage Heatmap | Generates an interactive HTML site map showing storage breakdown and hot/cold activity heatmap across all document libraries, lists, and site pages. Includes site-wide summary stacked bars and per-library click-through drill-downs. Saves the file to the site's document library and navigates the user directly to it. |

---

## Installing a Skill

Skills follow the [agentskills.io specification](https://agentskills.io/specification). The `Skills/` library in SharePoint is created automatically — install by uploading the skill folder into it.

1. Download the skill folder (e.g., `file-classifier/`)
2. In your SharePoint site, open the **Agent Assets** library
3. Navigate into the **Skills** folder (auto-created)
4. Upload the skill folder — the agent discovers it by the `name` field in `SKILL.md`

## Creating a Skill

A skill is a folder containing a `SKILL.md` plus supporting files. The folder lives inside a category subfolder and the folder name must match the `name` field in the `SKILL.md` frontmatter exactly.

### Where it goes

**In this repo:** `Skills/<category>/<skill-name>/`

**In SharePoint:** `Skills/<skill-name>/SKILL.md` — when uploading, take just the skill folder (not the category wrapper). Skip the `demo/` subfolder if there is one.

### Categories

Pick the category that best fits what the skill operates on or produces:

| Category | For skills that... |
|---|---|
| `ai/` | Are meta-skills — patterns, evaluation, self-improvement |
| `documents/` | Create or transform structured documents |
| `knowledge/` | Manage knowledge bases, research, expert routing |
| `libraries/` | Act on SharePoint document libraries (classify, organize, clean up) |
| `operations/` | Run business workflows, reports, or site-level analytics |
| `styling/` | Apply visual themes via list/column/view formatting |
| `writing/` | Generate or edit prose content |

If none fit, propose a new category in your PR description.

### Naming convention

- Folder name: **kebab-case** — lowercase, dash-separated (`organize-library`, not `OrganizeLibrary` or `organize_library`)
- The folder name must match the `name` field in `SKILL.md` exactly
- Be specific — avoid generic names like `tool`, `helper`, `processor`

### Required files

| File | Purpose |
|---|---|
| `SKILL.md` | Skill instructions with `name` and `description` frontmatter |
| `README.md` | Description, what you get, and contribution credits |
| `assets/sample.json` | Metadata for the PnP community samples gallery |
| `assets/preview.png` | Screenshot of the skill's output for the samples gallery (recommended 1280×720, 16:9, PNG) |

### Optional — demo content

If your skill benefits from a hands-on demo, add a `demo/` subfolder. Include a `README.md` with setup steps and a `sample-files/` folder with the content. Users uploading the skill to SharePoint can skip `demo/` — only `SKILL.md` is required for the skill to run.

---

## File templates

### `SKILL.md`

```markdown
---
name: summarize-page
description: Summarizes a SharePoint page in 3 bullet points.
  Use when the user asks for a quick summary of a page.
---

# Summarize Page

## Instructions

1. Read the full content of the specified page.
2. Identify the 3 most important points.
3. Return a bulleted summary, each bullet no longer than one sentence.
```

### `README.md`

```markdown
# Summarize Page

Short description of what the skill does and when to use it.

## What you get

- Bullet list of outputs and outcomes

## Contribution

| Property | Value |
|---|---|
| Author | Your Name |
| GitHub | [your-handle](https://github.com/your-handle) |
| First published | Month YYYY |
```

### `assets/sample.json`

```json
[
  {
    "name": "pnp-sharepoint-skills-summarize-page",
    "source": "pnp",
    "title": "Summarize Page",
    "shortDescription": "Summarizes a SharePoint page in 3 bullet points.",
    "url": "https://github.com/pnp/sharepoint-skills/tree/main/Skills/documents/summarize-page",
    "longDescription": [
      "Longer description spanning one or more paragraphs.",
      "Each array entry is rendered as a separate paragraph in the gallery."
    ],
    "creationDateTime": "2026-05-07",
    "updateDateTime": "2026-05-07",
    "products": [
      "SharePoint",
      "Microsoft 365 Copilot"
    ],
    "metadata": [
      { "key": "SAMPLE-TYPE", "value": "SharePoint-AI-Skill" },
      { "key": "SKILL-CATEGORY", "value": "Document Management" }
    ],
    "thumbnails": [
      {
        "type": "image",
        "order": 100,
        "url": "https://github.com/pnp/sharepoint-skills/raw/main/Skills/documents/summarize-page/assets/preview.png",
        "alt": "Summarize Page skill in action"
      }
    ],
    "authors": [
      {
        "gitHubAccount": "your-handle",
        "pictureUrl": "https://github.com/your-handle.png",
        "name": "Your Name"
      }
    ],
    "references": [
      {
        "name": "agentskills.io specification",
        "description": "The specification that SharePoint AI skills follow for installation and discovery.",
        "url": "https://agentskills.io/specification"
      }
    ]
  }
]
```

---

## Pre-submission checklist

Before opening your pull request, verify:

- [ ] Skill folder is inside the correct category subfolder (`Skills/<category>/<skill-name>/`)
- [ ] Folder name uses kebab-case and matches the `name` field in `SKILL.md` exactly
- [ ] `SKILL.md` has `name` and `description` in the frontmatter
- [ ] `README.md` follows the template (description, "What you get", Contribution table)
- [ ] `assets/sample.json` exists with the `url` and `thumbnails[0].url` pointing to your skill's actual path
- [ ] `assets/preview.png` exists and shows the skill's actual output (not a logo or placeholder)
- [ ] Skills work best when they are **focused** (one capability), **self-contained** (no external dependencies), and **discoverable** (clear `description` with trigger phrases)
