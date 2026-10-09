# n8n workflow exports

This directory contains versioned workflow JSON used by the optional n8n orchestration path.

## Import safely

1. Review the workflow JSON before importing it into an isolated n8n instance.
2. Configure credentials inside n8n's credential store; never put credential values in an export.
3. Require webhook authentication and keep the n8n editor and webhook private to the application network.
4. Disable execution-data retention for workflows that handle receipt images or sensitive payment evidence.
5. Test with synthetic receipts and Stripe test mode before enabling any live integration.

Exports use placeholder credential identifiers. Assign credentials inside your n8n instance after import. Workflow exports are code, not a production deployment recipe. Review node URLs, credential references, webhook paths, and execution settings for your own environment before use. Keep webhook secrets and customer data out of exported JSON and commit history.
