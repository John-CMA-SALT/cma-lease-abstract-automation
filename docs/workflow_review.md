# WORKFLOW_REVIEW
## Current Workflow
### Input:

User uploads one or more lease files to a dedicated Slack channel.

#### Trigger:

Zapier triggers on each new Slack message, parsing all attached files as an array.

#### Loop:

“Looping by Zapier” processes each file individually.

####OCR:

Each file is sent to PDF.co for OCR; output is a searchable PDF.

#### Collection:

All OCR’d file URLs are collected for further processing.

#### AI Extraction (Planned):

OCR’d files sent to OpenAI Lease Analyzer, which returns structured JSON.

#### Sheet Generation (Planned):

Data is mapped into a locked Google Sheets template (with formulas, named ranges, and QA checks).

### Output:

Finished sheet is shared via Slack and/or updated in Monday.com.

#### Error Handling (Planned):

Failures trigger alerts to a dedicated Slack channel.

### Known Issues & Considerations
Zapier test mode is limited; large OCR jobs require real-world runs.

File size/processing time: Large or poor-quality scans may take several minutes; recommend splitting huge files.

Slack file permissions: Slack/Zapier integration must have access to all files (should be fine with current permissions).

Security: API keys are stored in Zapier’s credential vault, not in logs.

Error handling: Needs to be added for robust notifications on failure.

Cleanup: Temporary file storage/variables should be cleared after runs.

### Recommended Next Steps
Finalize Google Sheets template (with locked formulas/named ranges).

Configure Zapier to collect OCR’d file URLs as an array for the AI extraction step.

Map OpenAI output into Google Sheets in a single, batch operation.

Build and test error-handler Zap.

Write staff SOP and training guide.
