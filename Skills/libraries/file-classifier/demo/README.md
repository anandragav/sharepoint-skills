# File Classifier — Demo Content

Demo content for the [file-classifier](../) skill. Use these sample files to set up a working demo of the skill in SharePoint.

## What's included

The `sample-files/` folder contains a mix of contracts, invoices, and purchase orders representing real document types the skill will classify.

## Setup

1. Create or open a SharePoint document library.
2. Upload all files from `sample-files/` into the library.
3. Install the [file-classifier](../) skill into your SharePoint Skills library (see the skill's README for install steps).
4. From a Copilot agent, ask: *"Classify the files in this library."*

## What to expect

The agent will:
- Create a `File classification` Choice column on the library
- Read each file's content and classify it as Contracts, Invoices, Purchase Orders, or Unclassified
- Create the appropriate metadata columns (5 per content type)
- Extract values from each file and populate the metadata columns
