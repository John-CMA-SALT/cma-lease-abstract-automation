+# Lease Abstract Automation: Workflow Review
+
+This document summarizes the current automation design, potential issues, and recommended next steps. It is based on the progress log provided in the project discussion.
+
+## Overview of the Planned Workflow
+
+1. **Input**: Staff upload all relevant lease files through a Google Form.
+2. **Zapier Loop**: For each uploaded file, download it from Google Drive and run PDF.co OCR to ensure the text is searchable.
+3. **OpenAI Analysis**: Upload all processed file IDs to the `Lease-Analyzer` assistant and request a single JSON response with key data fields.
+4. **Sheet Generation**: Copy the locked Google Sheets template (`LeaseAbstract‑TEMPLATE.gsheets`) and populate named ranges using the JSON values.
+5. **Output**: Share the filled sheet via Slack and optionally update monday.com.
+
+This approach keeps the dataflow within no-code tools and relies on built-in Zapier integrations.
+
+## Identified Issues and Considerations
+
+- **File Size Limits**: Google Forms restricts uploaded files to 10 MB each. Large scanned leases may need to be split or compressed before submission.
+- **Batching of Files**: Zapier delivers uploaded files as individual line items. The workflow must loop through each file, OCR it, and collect all resulting `file_id`s before calling OpenAI.
+- **OpenAI File Limits**: The API caps file uploads at 20 MB per file. Ensure the OCR step produces files below this threshold.
+- **Named Range Updates**: Google Sheets API supports batch updates to named ranges. Confirm whether a single batch call is used or one update per range; the latter increases Zap duration.
+- **Error Handling**: The current plan skips error notifications. Consider a secondary Zapier Manager trigger to alert Slack on failures.
+- **Security**: API keys (e.g., OpenAI) should be stored in Zapier's secure credentials, not in plaintext logs or repository files.
+
+## Recommended Next Steps
+
+1. Finalize the Google Sheets template with all required named ranges and formulas locked.
+2. Build Zapier steps to map the JSON fields into the sheet. Test using a small set of sample PDFs.
+3. Implement a clearing step for the temporary `lease_file_ids` storage key after each run.
+4. Add an error-handler Zap to post to a dedicated Slack channel when any step fails.
+5. Document SOP for staff, including guidance on file sizes and scanning quality.
+
