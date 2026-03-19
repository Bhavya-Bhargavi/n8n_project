
# Implementation Notes - n8n Workflow Assessment

## Overview
This workflow automates incident response by receiving webhooks, normalizing data, and notifying Slack and Office 365.

## Key Features
- **Data Normalization:** A JavaScript Code node validates inputs, maps P1-P4 severities to 1-4, and truncates descriptions to 240 characters.
- **Deduplication:** Implemented a file-based lock system in `submission/cache/` using the `dedupeKey` to ensure idempotency.
- **Reliability:** Configured HTTP Request nodes with 5 retries and exponential backoff to handle mock server errors (429/500).


## How to Test
1. Start the mocks: `npm run mocks`
2. Import `workflow.json` into n8n.
3. Trigger the workflow:
   `Invoke-RestMethod -Method Post -Uri "http://localhost:5678/webhook-test/incident" -ContentType "application/json" -InFile "fixtures/incidents/INC-10001.json"`