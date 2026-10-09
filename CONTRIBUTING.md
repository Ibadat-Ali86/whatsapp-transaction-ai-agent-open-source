# Contributing

Thanks for helping improve the WhatsApp Transaction Verification Agent. Changes should preserve conservative payment decisions, protect customer data, and remain reproducible without production credentials.

## Before you start

- Open an issue for substantial changes so the expected behavior can be agreed on.
- Do not use a client's WhatsApp account, Stripe account, real receipt, or production service for local development or CI.
- Use synthetic fixtures and test credentials only.
- Keep client names, account identifiers, service URLs, screenshots, credentials, session state, and production runbooks out of commits.

## Development setup

Follow the isolated local setup in the [README](README.md). Use Node.js 20 or newer and Python 3.12. Do not enable live Stripe verification or connect a live WhatsApp session while developing.

## Changes and review

- Keep changes focused and preserve existing module boundaries.
- Validate input at service boundaries and treat OCR or model output as untrusted evidence.
- Preserve fail-closed behavior for ambiguous, unmatched, duplicate, and technically unavailable verification results.
- Add or update regression coverage for behavior changes, using synthetic inputs.
- Update user-facing documentation when configuration or behavior changes.
- Never include secrets, customer data, or private deployment details in commits, test output, or pull request text.

## Before opening a pull request

Run the relevant checks from the README and include their results. Review the complete diff for credentials, personal data, session material, generated files, and unrelated changes. Do not claim that a check passed unless it ran successfully.

By submitting a contribution, you confirm that you have the right to submit it under the project's [MIT License](LICENSE).
