# Contributing to Trade Calculator Configs

Thank you for helping keep broker templates accurate and up-to-date!

## Adding a New Broker

1. **Fork** this repository
2. **Create** a new file: `templates/brokers/your-broker.json`
3. **Use** the template structure below
4. **Add** an entry to `templates/manifest.json`
5. **Validate** your changes locally
6. **Submit** a Pull Request

## Template Structure

```json
{
  "$schema": "../../schemas/broker-template.schema.json",
  "broker": {
    "id": "broker-id",
    "name": "Broker Display Name"
  },
  "version": "2026-04-08",
  "contributors": ["your-github-username"],
  "sources": ["https://broker-website.com/charges"],
  "disclaimer": "Community-maintained. Verify with official sources.",
  "segments": {
    "equity_delivery": { ... },
    "equity_intraday": { ... },
    "equity_futures": { ... },
    "equity_options": { ... },
    "currency_futures": { ... },
    "currency_options": { ... },
    "commodity_futures": { ... },
    "commodity_options": { ... }
  }
}
```

## Segment Charge Structure

Each segment must include:

```json
{
  "brokerage": {
    "type": "flat" | "percentage" | "per_order",
    "value": 0,
    "minValue": 0,    // optional
    "maxValue": 20    // optional
  },
  "stt": { "buyRate": 0, "sellRate": 0.1 },
  "exchangeCharges": { "nseRate": 0.00297, "bseRate": 0.00375 },
  "sebiCharges": 10,
  "gst": 18,
  "stampDuty": { "rate": 0.015 },
  "dpCharges": 15.93,  // only for equity_delivery
  "ipftCharges": { "rate": 10, "unit": "crore", "includesGst": false }
}
```

## Brokerage Types

| Type | Description | Example |
|------|-------------|--------|
| `flat` | Fixed amount per trade | `{ "type": "flat", "value": 0 }` |
| `percentage` | % of turnover with optional min/max | `{ "type": "percentage", "value": 0.03, "maxValue": 20 }` |
| `per_order` | Fixed amount per order | `{ "type": "per_order", "value": 20 }` |

## Guidelines

- ✅ Use lowercase-hyphenated filenames: `broker-name.json`
- ✅ Include `sources` with official URLs where rates were found
- ✅ Set `version` to the date you verified the rates (YYYY-MM-DD)
- ✅ Add your GitHub username to `contributors`
- ✅ Test with the app before submitting
- ❌ Don't use actual broker trademarks in template IDs
- ❌ Don't submit without verifying against official broker documentation

## Updating Existing Templates

1. Update the charge values
2. Update the `version` date
3. Add your username to `contributors` (if not already there)
4. Add/update `sources` with verification URL
5. Submit PR with description of what changed

## Validation

PRs are automatically validated via GitHub Actions. You can also validate locally:

```bash
npm install
npm run validate
```

## Questions?

Open an issue if you have questions about the template format or need help.
