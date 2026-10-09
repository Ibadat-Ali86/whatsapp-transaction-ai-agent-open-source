# WhatsApp Transaction Verification Agent

A self-hosted reference implementation for processing payment receipt images sent through WhatsApp, extracting evidence, and checking eligible payments against Stripe.

## What it does

The service accepts receipt images from configured WhatsApp groups, extracts text with Tesseract, and can use a configured vision provider when local OCR is insufficient. An optional n8n workflow routes verification requests. Stripe lookups compare the available receipt evidence with payment records. The bot returns a result or routes uncertain cases for human review.

The system is designed to fail closed: an ambiguous or unmatched payment is not treated as verified, and technical failures must remain distinguishable from a payment rejection. Model-generated extraction is evidence only; it is not payment authorization.

## Architecture

```text
WhatsApp
   -> Node.js bot and group allowlist
   -> bounded media handling and durable processing queue
   -> OCR service (Tesseract; optional cloud vision provider)
   -> optional n8n orchestration
   -> Stripe verification
   -> verified, duplicate, review-required, or technical-failure response
```

See [the architecture overview](docs/ARCHITECTURE.md) for the component boundaries and data flow.

## Technology

- Node.js 20 or newer for the WhatsApp bot
- Python 3.12 for the OCR and Stripe verification services
- Tesseract OCR
- Optional n8n workflow orchestration
- Stripe API for payment evidence checks

## Local development

Use synthetic fixtures, a dedicated WhatsApp test account, an isolated test group, and Stripe test mode. Do not connect this checkout to a client account or production data.

```bash
npm ci
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
cp .env.example .env
```

Set only the credentials needed for an isolated test environment. Keep `.env`, WhatsApp session state, screenshots, logs, and service-account files out of Git. Optional cloud vision providers transmit image content to their service; review the provider's terms and data handling before enabling one.

## Checks

```bash
npm run test:whatsapp
python -m pytest tests/unit/ tests/integration/
```

For the n8n adapter smoke check, start an isolated local OCR/n8n setup and use synthetic input:

```bash
npm run smoke:n8n
```

The smoke command requires a local authenticated n8n webhook. It does not establish that an external or production deployment is healthy.

## Security and privacy

Payment screenshots can contain personal and financial information. Use synthetic data for development, minimize retention, keep service ports private, and never paste credentials, session files, or real customer receipts into issues or pull requests. Read [Security](SECURITY.md) before reporting a vulnerability.

Source code and tests do not constitute a security audit, production support commitment, or compliance certification. Review the intended release contents and Git history with a dedicated secret scanner before publishing.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development and review expectations. Before opening a pull request, confirm that it contains no production data, client identifiers, credentials, or private operational material.

## License

This project is licensed under the [MIT License](LICENSE).
