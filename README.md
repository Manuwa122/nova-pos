# ✦ NovaPOS

Modern, responsive, browser-based point of sale demo. Built to deploy on **Vercel** without a backend.

## Languages
- English / සිංහල switch in the top-right corner; persists per browser.
- Core navigation, checkout, inventory, settings, sales and receipt interface translations. Product names remain as entered; receipt translations are a demo feature and should be reviewed before commercial printing.
- Sinhala glyph rendering uses available system fonts; install a Sinhala-capable font on devices if needed.

## Features
- Product search and category filters
- Fast cart and checkout, tax calculation, cash/card/bank-transfer recording
- Printable receipts and sales history
- Inventory management with stock deductions
- Dashboard with revenue, orders and stock alerts
- CSV transaction export and JSON backup/restore
- Mobile-friendly interface; Sri Lankan rupees (LKR) by default

## Quick start
Open `index.html` in a modern browser, or run `python -m http.server 8000` and visit `http://localhost:8000`.

## Deploy
1. Create a GitHub repository called `nova-pos`.
2. Upload `index.html`, `README.md`, and `vercel.json`.
3. Vercel → Add New → Project → Import `nova-pos` → Deploy. Framework: **Other**, no build command.

## Roadmap informed by established POS systems
- Next priorities: barcode SKU scanning, product discounts, refunds/returns, hold/resume orders, cashier roles, audit trail, and cloud sync.
- Research references: https://loyverse.com/features and https://help.loyverse.com/help/how-change-language . These advanced features are **not implemented** in the demo.

## Important limitation
This is a **single-browser local demo**, not production-ready POS software. Data lives in browser localStorage and does **not** synchronize across devices; clearing browser data deletes local records unless backed up. No user authentication, server-side audit trails, real payment gateway, fiscal compliance, or multi-cashier access. Payments are only **recorded**, never processed. For production use add a secure database (e.g. Postgres), auth/roles, server-validated order logic, device synchronization, backups and receipt/legal requirements before use.