# RateX — Dental Quotation Generator

A single-page quotation tool for international dental treatment packages, with **live currency conversion** built in.

**Live app:** https://wsiyal.github.io/ratex/

## What it does

- Build a treatment quotation from a categorized price list (implants, crowns, veneers, orthodontics, etc.)
- Converts the RMB total to the client's currency automatically
- Exchange rates are fetched from live market-rate APIs on load and refreshed every 30 minutes, with a status indicator showing whether the rate is **live**, **cached** (last known rate, used offline), or a **preset estimate** (fallback if no rate source is reachable)
- The rate field stays editable — override it manually any time and the auto-refresh won't touch it again for that currency until you hit "Refresh"
- Supports 16 preset currencies plus a free-text "Other country" option
- Copy a plain-text summary, or use Print / Save PDF to produce a client-ready quotation
- Works fully offline (falls back to the last cached or preset rate) — only the live-rate refresh needs a connection

## Live exchange rates

Rates are RMB (CNY)-based and pulled, in order, from:

1. [open.er-api.com](https://www.exchangerate-api.com/docs/free) (v6, no key required)
2. [api.exchangerate-api.com](https://www.exchangerate-api.com/) (v4, no key required)
3. [@fawazahmed0/currency-api](https://github.com/fawazahmed0/exchange-api) via jsDelivr (daily-updated static data, no key required)
4. The last successfully fetched rate, cached in the browser (`localStorage`)
5. A built-in preset estimate, used only if none of the above are reachable

All three live sources are free, keyless, and CORS-enabled for client-side use, so the app has no backend and no secrets to manage.

## Running locally

It's a static site — no build step.

```bash
python -m http.server 8765
```

Then open http://localhost:8765.

## Deploying

The `main` branch is served directly by GitHub Pages from the repository root.

## Notes

- Prices are sourced from the "海外价目册20260804" internal price list (4 August 2026) — verify any special case or unlisted price before sending a quotation to a client.
- This tool gives a preliminary estimate. Final treatment plans and prices are confirmed after an in-person examination, and currency conversion for actual payment is calculated at the rate applicable on the payment date.
