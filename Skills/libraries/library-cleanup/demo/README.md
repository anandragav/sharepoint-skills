# Library Cleanup — Demo Content

Demo content for the [library-cleanup](../) skill. Use these sample files to set up a working demo of the skill in SharePoint.

## What's included

The `sample-files/` folder contains an intentionally messy library structure with:
- Duplicate files in multiple folders
- Files with bad names (`asdfghjkl.pdf`, `doc1.docx`, `final_FINAL_v3 (2).pdf`)
- Empty or near-empty folders
- Excessive nesting

## Setup

1. Create or open a SharePoint document library.
2. Upload the entire folder structure from `sample-files/` into the library, preserving folders.
3. Install the [library-cleanup](../) skill into your SharePoint Skills library.
4. From a Copilot agent, say: *"clean up file demo"*

## What to expect

The agent will:
- Scan the library and report issues (duplicates, bad names, empty folders, nesting depth)
- Calculate an Organization Score (0–100) for the current state
- Read file content to propose meaningful, content-based rename suggestions
- Show a before/after comparison with a visual chart
- Execute the cleanup with a live TODO checklist after your approval
- Generate an HTML impact dashboard at the end
