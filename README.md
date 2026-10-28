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

## v1.2 — Shop branding & advanced receipts

- Shop profile: name, contact phone, email, postal address and thank-you message.
- Automatic deterministic SVG shop logo based on the shop name (no external AI service, assets or logo upload required).
- Itemized print/PDF-friendly receipt with invoice number, date, payment method, products, quantity, unit price, line totals, order discount, configured tax, total, amount received and change.
- Sale-time shop information is preserved on new sales for consistent historical receipts.
- Product SKU/barcode fields and search by name or code. Barcode readers that act as keyboards may enter codes through the search field; camera scanning is not yet implemented.
- Percentage order discounts, printed and stored per sale. There is no integrated bank/card payment processing.

**Limitations:** Demonstration with browser-local data only. Changing computers or browsers does not synchronize transactions. User permissions, refunds, suppliers, accounting, payment integrations, and fiscal/tax compliance require further work. Sample products are illustrative, not a real inventory. Receipt tax is configurable and not legal/tax advice.

### POS feature research

The feature direction was informed by product documentation for [Shopify POS](https://help.shopify.com/en/manual/sell-in-person/shopify-pos), [Lightspeed Retail](https://www.lightspeedhq.com/pos/retail/features/) and [Square item modifiers](https://squareup.com/help/us/en/article/5119-create-and-manage-item-modifiers). Planned future modules include supplier purchase orders, returns/refunds, customer profiles, roles/permissions and cloud inventory synchronization; **these are not yet implemented**.

## Barcode scanners & POS hardware (v1.3)

- **USB / Bluetooth scanner:** Configure your scanner to **USB HID / keyboard wedge** mode and to append **Enter (CR)** after every scan. On the POS screen use the dedicated barcode field (or press **F2** to focus it). Products are matched by exact `barcode` or `sku`, and one unit is added per valid scan. Press **F4** to search product names manually.
- **Barcode setup:** Add products under Inventory and enter their barcode values. Test a scan in Notepad: it should type the code and end with Enter. Bluetooth scanners must first be paired in the device operating system.
- **Receipts:** Use Print / Save PDF and your device's installed printer driver. An 80mm paper rule is included in the printable bill; review margins and paper settings in the browser print dialog. Silent printing, automatic cash drawer opening, and raw ESC/POS control are **not implemented**.
- **POS terminals and tablets:** Works as a responsive web interface in modern browsers. Touchscreen operation is supported by ordinary browser buttons, subject to the device/browser. Printer, scanner and payment-terminal compatibility varies by model, firmware, OS and browser.
- **Payment terminals:** The `Card` payment option is record-keeping only. It does **not** charge a bank card or connect to an EFTPOS terminal. Payment processing requires a supported certified payment provider integration.
- **Storage caution:** Sales and stock are browser-local, **not synchronized between multiple devices**. Do not run separate cashiers as though they share stock. A cloud database, account-based access, synchronization and backups are required for multi-register commercial use.