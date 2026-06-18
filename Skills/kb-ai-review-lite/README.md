# KB AI Review Lite

Performs a lightweight AI quality-check pass on one or more KB documents in a SharePoint
document library. Validates factual accuracy against category-specific sources, writes
structured review output as metadata, sets review status, scores the document, and
schedules the next review date — all without touching the original file content.
Designed for Microsoft 365 Copilot experiences in SharePoint.

![preview](./assets/preview.png)

## What you get

- AI-generated review summary per KB document written directly to library metadata
- Structured Markdown draft payload with findings, evidence, proposed updates, and risks
- Color-coded **AI Review State** column (green = Review Complete, blue = Published, orange = Not Run)
- **Review Score** displayed as a percentage bar (green ≥80, orange ≥50, red <50)
- Automatic **KB Category** classification (Security, Infrastructure, Applications, General, Other)
- **Next Review Date** calculated per category cadence (Security 30 days, Infrastructure 60 days, all others 90 days)
- Quality gates that prevent incomplete or generic output from being written back
- All 9 review columns created automatically on first run with correct names and types

## When to use

Ask Copilot any of the following (or close variations):

- *"run kb-ai-review-lite on the selected KBs"*
- *"review these KB files"*
- *"run AI review"*
- *"create AI review columns and summarize"*
- *"generate review notes"*

Works on any SharePoint document library containing KB documents in Word, PDF, or
plain text format. The skill reads file content and validates factual claims — it works
best on documents with concrete values such as URLs, version numbers, ports, timeouts,
phone numbers, and procedural steps.

---

## Prerequisites

- Copilot license enabled for Microsoft 365
- AI in SharePoint enabled on the target site (opt-in required during public preview)
- Contributor permissions on the target library

---

## First Run Behavior

On the **first run** against a new library, the skill will:

1. Create all 9 required review columns with the correct names and types
2. Stop and display a setup notice asking you to change one setting on two columns
3. Provide exact step-by-step instructions for that change

**You must complete this manual step before the review can run:**

1. Go to **Library Settings** → **Columns**
2. Click **AI Review Summary**
   - Find **Allow unlimited length in document libraries**
   - Select **Yes** → **Save**
3. Click **AI Draft Payload**
   - Find **Allow unlimited length in document libraries**
   - Select **Yes** → **Save**

Once saved, run the skill again. The review will proceed immediately — this step is
not required on any subsequent run.

If you are new to SharePoint column settings, use the example below when enabling
**Allow unlimited length in document libraries** for both **AI Review Summary** and
**AI Draft Payload**:

<img src="./assets/SharePointMultipleLIneTextSetting.png" alt="SharePoint multi-line text column setting" width="60%" />


> **Why is this step required?**
> SharePoint's AI skill platform cannot set the `UnlimitedLengthInDocumentLibrary`
> property during column creation. This is a known platform limitation as of June 2026.
> Without this setting, both columns default to a 255-character cap, which is insufficient
> for AI-generated review output. The skill detects this condition automatically and
> stops before writing any data.

---

## Columns Created

| Display Name | Internal Name | Type | Notes |
|---|---|---|---|
| AI Review State | `AIReviewState` | Choice | Review Complete / Not Run / Published |
| AI Review Summary | `AIReviewSummary` | Note | Requires unlimited length — see First Run |
| AI Draft Payload | `AIDraftPayload` | Note | Requires unlimited length — see First Run |
| Completed On | `CompletedOn` | DateTime | UTC timestamp of last review |
| Reviewed By | `ReviewedBy` | Text | Agent or user display name |
| Review Score | `ReviewScore` | Number | 0–100, displayed as percentage bar |
| Failure Reason | `FailureReason` | Note | Blank on success |
| Next Review Date | `NextReviewDate` | DateTime | Calculated from category cadence |
| KB Category | `KBCategory` | Choice | Security / Infrastructure / Applications / General / Other |

---

## SharePoint Skill

| Solution | Author(s) |
| --- | --- |
| kb-ai-review-lite | Andrew Burns &#124; [GitHub](https://github.com/GeorgiaGit) &#124; [LinkedIn](https://www.linkedin.com/in/andrewkburns/) |

## Version history

| Version | Date | Comments |
| --- | --- | --- |
| 1.0 | June 2026 | Initial Release |

## Disclaimer

**THIS CODE IS PROVIDED _AS IS_ WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING ANY IMPLIED WARRANTIES OF FITNESS FOR A PARTICULAR PURPOSE, MERCHANTABILITY, OR NON-INFRINGEMENT.**

<img src="https://m365-visitor-stats.azurewebsites.net/sharepoint-skills/skills/kb-ai-review-lite" />

