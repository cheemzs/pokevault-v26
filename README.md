# PokéVault v26.0

Pokémon card & sealed product portfolio tracker with live TCG prices, price history charts, graded card market data, trade analyser, P/L dashboard, and public portfolio sharing.

## What's new in v26

### Graded card chart system (ported from v17.0)
- **Dynamic grade chips** — the card detail chart row now renders grade buttons based on what `salesByGrade` data the API actually returns, instead of hardcoded PSA 10 / PSA 9 / BGS 10 buttons.
- **All grades supported** — PSA 10/9/8/7, BGS 10/9.5/9, CGC 10/9.5/9, SGC 10/9, and any future grades the API returns.
- **Compare all** — overlay multiple grades on one multi-line chart to compare market prices side by side.
- **Single fetch** — one API call with `includeEbay=true` fetches all grade data at once (vs. a separate call per grade in v25).
- **Colour-coded chips** — each grading company has a distinct colour (PSA amber, BGS purple, CGC teal).

### Share Portfolio button layout fix
- Removed "Share Portfolio" from the metrics grid (it was causing a second row to wrap on most screens).
- The 🔗 Share button in the header toolbar still works identically.

## Stack

- **Frontend**: Vanilla HTML/CSS/JS (no build step)
- **Backend**: Vercel serverless functions (`/api/*.js`)
- **Database**: Supabase (Postgres)
- **Prices**: PokémonPriceTracker API v2 with eBay graded sales data

## Deployment

1. Push to a GitHub repo
2. Import into Vercel
3. Set environment variables in Vercel dashboard:
   - `POKEPRICE_API_KEY` — PokémonPriceTracker API bearer token
   - `SUPABASE_URL` — your Supabase project URL
   - `SUPABASE_SERVICE_KEY` — Supabase service_role key
   - `SUPABASE_ANON_KEY` — Supabase anon/public key
4. Deploy

## Supabase schema

Run `supabase_schema_v26.sql` against your Supabase project. No schema changes from v25 — the graded chart data is fetched live from the API each time the card detail modal opens.

## API endpoints

| Endpoint | Method | Notes |
|---|---|---|
| `/api/pokeprice` | GET | Proxies PokémonPriceTracker API. Pass `includeEbay=true` for graded data. |
| `/api/search` | GET | Card search helper |
| `/api/portfolio` | GET/POST/PATCH/DELETE | Portfolio CRUD (requires auth) |
| `/api/auth` | POST | Auth helper |
| `/api/graded` | GET | Legacy endpoint (unused in v26) |
