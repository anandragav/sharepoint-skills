# File Classifier

Classifies files in a SharePoint document library by reading their content and matching them to known content types (Contracts, Invoices, Purchase Orders). Creates the appropriate metadata columns, extracts values from each file, and saves them automatically.

## What you get

- Files classified into **Contracts**, **Invoices**, or **Purchase Orders** based on document structure — not just keywords
- 5 metadata columns created per content type (identifier, key party, critical date, financial amount, status)
- Metadata extracted from file content and written automatically
- A `File classification` Choice column with a metadata extraction prompt for future autofill

## Demo content

Sample files for trying this skill end-to-end are in the [demo/](./demo/) subfolder. Includes a mix of contracts, invoices, and purchase orders to upload to a library before running the skill. Skip this folder when uploading the skill to SharePoint.

## Contribution

| Property | Value |
|---|---|
| Author | Joe Komban |
| GitHub | [JoeFranc](https://github.com/JoeFranc) |
| First published | May 2026 |
| Presented at | Microsoft 365 Community Conference 2026 |
