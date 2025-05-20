# cma-lease-abstract-automation
Workflow for processing files (of varying format) for a CRE lease into a lease abstract
# CMA Lease Abstract Automation

This repository tracks the design documents for an automated workflow that converts lease files (PDFs or images) into a structured Google Sheet. The build uses no-code tools such as Zapier, Google Forms, PDF.co, OpenAI, and Slack.

All automation steps are orchestrated through Zapier. Incoming files are OCR‑processed, analyzed by the `Lease‑Analyzer` assistant, and then mapped into a Google Sheets template that contains formulas for the rent schedule and QA checks.

Documentation is located in the `docs/` folder.
