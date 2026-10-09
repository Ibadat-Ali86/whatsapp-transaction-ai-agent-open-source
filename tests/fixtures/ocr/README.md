# OCR Test Fixtures

This directory contains labeled, synthetic fixtures for OCR development and evaluation. Never add payment screenshots, logs, or other data copied from production or a client.

Each fixture is a **pair of files**:

```
<name>.png    ← the screenshot image (synthetic/approved only)
<name>.json   ← the expected extraction result
```

## Expected JSON Format

```json
{
  "email": "testuser@example.com",
  "amount_cents": 2500,
  "minutes": "31",
  "payment_date": "2026-09-09",
  "customer_name": "Test User",
  "status": "Completed"
}
```

**Field rules:**
- `amount_cents` — **integer cents only** (`$25.00` → `2500`). Never float.
- `minutes` — two-digit string `"00"`–`"59"`. Null if not present.
- `payment_hour` — local payment hour in 24-hour form (`0`–`23`). Null if not present.
- `payment_date` — ISO 8601 `YYYY-MM-DD`. Null if not present.
- Any field may be `null` if genuinely absent from the screenshot.

## Safety

- Keep every image and expected result synthetic, with invented names, addresses, amounts, and transaction details.
- Do not add client or production records, even if names or identifiers appear partly obscured.
- Local raw-image directories are excluded from version control; do not weaken those ignore rules.

## Running the Benchmark

```bash
python -m tests.accuracy.benchmark
```

Use only synthetic fixtures when running local evaluation. Confirm the benchmark's configured providers before running it if network access is enabled.
