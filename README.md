# PokéVault v15

Live Pokémon card price tracker and investment portfolio manager.

## What's new in v15

### 1. Mark as Sold
Each active portfolio row now has a **$ Sell** button. Clicking it opens a modal where you enter:
- **Sold Price (SGD)** — total amount received for the lot
- **Date Sold**

The row is then updated in `portfolio_items` with `sold = true`, `sold_price`, and `sold_date`. Sold items disappear from the Portfolio table (they move to Past Transactions in the P/L Dashboard).

### 2. Two-Tab P/L Dashboard
Click the **P/L Dashboard** metric card to open a full overlay with two tabs:

## Tech stack
- Vanilla JS + Chart.js (no framework)
- Supabase (Postgres + Auth + RLS)
- Vercel (serverless API routes in `/api`)
- TCGPlayer / PokePrice API via `/api/pokeprice.js`
