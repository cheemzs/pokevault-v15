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

| Tab | What it shows |
|-----|---------------|
| **Current Portfolio** | All active (unsold) cards with their unrealised P/L, cost basis, current value, and ROI % |
| **Past Transactions** | All sold items sorted by date, showing cost basis, sale price, and **realised P/L**. Plus a **Lifetime Total P/L** banner at the top. |

> **Key distinction:** The Portfolio table on the main page is purely your *holdings* (what you own). P/L is always computed on the fly and summarised in the Dashboard — it is never stored as a column.

### 3. Chart shows Raw price
The price history chart in the Card Detail modal always uses the **raw market price** (not the graded eBay price), regardless of the card's grade. This gives you a clean, consistent view of fair market value over time.

---

## Supabase setup

Run `supabase_schema_v15.sql` in your Supabase SQL Editor.

**Key schema points:**
- `portfolio_items.sold = false` → active holding (Tab 1 / Portfolio table)
- `portfolio_items.sold = true` → closed position (Tab 2 / Past Transactions)
- `sold_price` stores the **total SGD received** for the whole lot
- P/L is never stored — always computed: `(sold_price - purchase_price * quantity)` for realised, `(current_value - purchase_price) * quantity` for unrealised

---

## Deploy to Vercel

```bash
git init
git add .
git commit -m "feat: pokevault v15"
git remote add origin https://github.com/YOUR_USERNAME/pokevault-v15.git
git push -u origin main
```

Then connect the repo to Vercel. No environment variables needed — Supabase keys are in `app.js`.

---

## Tech stack
- Vanilla JS + Chart.js (no framework)
- Supabase (Postgres + Auth + RLS)
- Vercel (serverless API routes in `/api`)
- TCGPlayer / PokePrice API via `/api/pokeprice.js`
