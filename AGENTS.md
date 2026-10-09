# Repository guidance

## Scope and safety

- Keep client identity, production configuration, credentials, WhatsApp session state, payment screenshots, logs, and private operational documentation out of public commits.
- Do not connect development tools or validation commands to production WhatsApp, Stripe, n8n, or cloud services.
- Treat image OCR and model output as untrusted evidence. Preserve fail-closed behavior for uncertain payment matches.
- Do not modify or deploy production infrastructure as part of repository work.

## Architecture navigation

Use Graphify for codebase navigation when its graph is available:

1. Run `graphify query "<focused question>"` for a scoped code map.
2. Use `graphify path "<symbol A>" "<symbol B>"` for call relationships and `graphify explain "<symbol>"` for a focused component.
3. If no graph exists, run `graphify update . --no-cluster` to build the local AST graph. This does not require an LLM API key.
4. Keep generated `graphify-out/` files local; do not commit them unless maintainers explicitly decide otherwise.

## Project checks

- JavaScript: `npm run test:whatsapp`
- Python: `python -m pytest tests/unit/ tests/integration/`
- n8n adapter: `npm run smoke:n8n` against an isolated local instance and synthetic data only.

Report exactly which checks ran. Never include secret values or production records in tool output, documentation, or pull requests.
