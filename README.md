# LedgerOS v5.0

**Complete privacy-first bookkeeping software** for freelancers and small businesses.

Runs entirely in your browser. No accounts, no cloud, no tracking. All data stays on your device until you choose to export or sync it yourself.

![LedgerOS](https://img.shields.io/badge/version-5.0-c9963a) ![PWA](https://img.shields.io/badge/PWA-ready-2eb87a) ![Offline](https://img.shields.io/badge/offline-first-3b7ef6)

---

## Features

### Sales
- **Clients** — contact management
- **Estimates / Quotes** — create, send status, convert to invoice in one click
- **Invoices** — line items, tax, due dates, status (draft / pending / paid / overdue), multi-currency, PDF export

### Purchases
- **Vendors** — supplier directory
- **Purchase Orders** — line items, status, one-click "Receive → Bill"
- **Bills (Accounts Payable)** — track what you owe, due dates, mark paid
- **Expenses** — categorized, recurring flag, vendor tracking
- **Inventory** — product register with SKU/cost/price/stock, stock movements, and COGS fed into the P&L report

### Accounting
- **Chart of Accounts** — standard small-business CoA (Assets, Liabilities, Equity, Income, Expenses)
- **Journal Entries** — true multi-line double-entry (any number of debit/credit lines, must balance)
- **Reports** — Profit & Loss (with COGS), Balance Sheet, Trial Balance, Sales by Client, Tax Summary, Accounts Receivable Aging — each exportable as a real PDF

### People
- **Employees** — role, pay type (salary / hourly), rate, status
- **Payroll** — bi-weekly pay runs with gross / estimated tax / net, history & YTD

### Finance
- **Banking** — bank & card accounts, CSV transaction import, match transactions to invoices/bills/expenses, full reconciliation workflow with cleared-balance checking
- **Tax Center** — GST / HST / PST settings, period-based collected vs. input-tax-credit calculation, net owing/refund, filing history log (estimates only — always confirm with a tax professional)
- **Fixed Assets** — asset register with straight-line depreciation, accumulated depreciation and book value tracking
- **Receipts (with OCR)** — snap or upload a photo/PDF receipt; images are scanned automatically to guess vendor, amount and date, then create a linked expense in one click
- **Cash Flow Forecasting** — 30/60/90-day projected balance from open invoices, unpaid bills, recurring expenses and average payroll, with a warnings panel and chart
- **AI Accountant** — offline, rule-based insights (why profit changed, expense category shifts, top clients, overdue invoices, payroll affordability, cash runway, collection speed, client concentration risk, vendor spend, budget variance, anomaly detection) with a free-text question box — nothing leaves your device

### Planning
- **Budgets** — Business mode + Personal mode with separate categories
- **Spreadsheet** — lightweight grid with `=SUM()`, `=AVG()`, `=COUNT()`, `=MAX()`, `=MIN()`, cell references, CSV export
- **Recurring** — templates that auto-generate invoices, bills or expenses on a weekly/monthly/quarterly/yearly schedule

### System
- **Multi-Business** — switch between completely separate sets of books (own clients, invoices, chart of accounts, everything) from the sidebar
- **Multi-Currency** — invoice clients in any currency with a per-invoice exchange rate; the invoice itself shows the native currency, while dashboards/reports convert to your base currency for consistent totals
- **Document Attachments** — attach files (contracts, receipts, PDFs) to invoices, bills, expenses, vendors and purchase orders
- **Audit Trail** — every create/edit/delete across the business, logged automatically with who/what/when (last 500 events)
- **Roles** — Owner/Admin/Bookkeeper/Accountant/Employee/Read-Only modes that hide irrelevant menus and, for Read-Only, block saving. This is a local convenience for handing off the device, **not real security** — there's no server here to enforce it
- **Sync (via a file you control)** — link one JSON file (via the File System Access API) that you can put in a Dropbox/Drive/iCloud folder to carry data between your own devices. This is a manual save/load to a shared file, not live multi-user sync
- Dark / light mode
- Global search (⌘/Ctrl + K)
- Keyboard shortcuts (`?` for help)
- Full JSON backup / restore
- Installable PWA + offline support (see caveats below for OCR/PDF)
- Mobile responsive + bottom navigation

---

## Quick Start

1. Open `ledgeros.html` in a modern browser (Chrome, Firefox, Safari, Edge).
2. Or serve the folder with any static server for the best PWA experience:

```bash
# Example with Python
python -m http.server 8080

# Example with npx
npx serve .
```

3. On first load you'll see sample data and an onboarding modal.
4. Go to **Settings** → update your business name, tax rate, currency, role, etc.

---

## File Structure

```
.
├── ledgeros.html    # The entire application (single file)
├── manifest.json    # PWA manifest
├── sw.js            # Service worker (offline + caching)
└── README.md        # This file
```

Everything lives in one HTML file for maximum portability. No build step required.

---

## Data & Privacy

- All data is stored in **localStorage**, namespaced per business (`lo2_...` for your default business, `lo2_biz_<id>_...` for additional ones).
- Nothing is sent to any server, with one narrow exception: Receipt OCR and the jsPDF/Chart.js libraries are fetched from a CDN (cdnjs) the first time you use them. Your actual data — receipt images, financial records — is never uploaded anywhere; only the *code* to run OCR/PDF/charts locally is downloaded.
- Use **Settings → Export All Data** to download a full JSON backup, or **Settings → Sync** to link a file you keep in your own cloud-synced folder.
- Use **Settings → Import Data** (or Sync → Load) to restore from a backup.
- **Clear All Data** resets the current business to a blank slate.

### Backed-up entities
Clients · Invoices · Estimates · Expenses · Vendors · Bills · Purchase Orders · Products · Stock Movements · Chart of Accounts · Journal · Employees · Pay Runs · Bank Accounts · Bank Transactions · Fixed Assets · Receipts · Tax Settings · Tax Filings · Recurring Templates · Attachments · Currencies · Audit Log · Budgets · Spreadsheet · Settings

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `⌘ / Ctrl + K` | Open global search |
| `Esc` | Close modal / search |
| `?` | Show keyboard help |

---

## Design System

**Ink & Brass** — dark navy ink, warm brass accents, clean serif headings (DM Serif Display), modern sans body (Outfit), monospace numbers (DM Mono).

Full dark mode support with carefully tuned surfaces and borders.

---

## Technical Notes & Honest Limitations

- **Double-entry**: Journal entries support any number of debit/credit lines and must balance before posting. Account balances update automatically.
- **Payroll**: Simplified estimate (flat ~20% deduction). Not a substitute for real payroll software or a CPA.
- **Tax Center**: estimates GST/HST/PST by applying your configured rate to invoice and expense totals for the selected period. It does not know which specific expenses actually included tax — always verify before filing.
- **Fixed Assets**: straight-line depreciation only.
- **Cash Flow Forecasting**: projects from open invoices, unpaid bills, recurring expenses and your historical average pay run — not a guarantee of future cash position.
- **Multi-Currency**: contained to invoices. Exchange rates are entered manually (Settings → Manage Currencies) since the app is offline-first and can't fetch live rates; each invoice snapshots the rate at creation time so past invoices don't shift when you update a rate later. Bills and expenses are currently single-currency (in your base currency).
- **Multi-Business**: a brand-new business starts with a clean Chart of Accounts and no demo data. Switching businesses reloads the page to guarantee a clean state.
- **Roles**: a convenience UI mode only — it hides menus and blocks the Read-Only role from saving, but anyone with access to the device can switch their own role back. There is no authentication and no server, so this is not a security boundary.
- **Sync**: uses the File System Access API (Chromium-based browsers only — Chrome, Edge). It links one file for the current browser session; refreshing the page requires re-linking. It is a manual, single-writer save/load, not real-time multi-user sync — there's no backend here to build that on top of.
- **Receipt OCR**: runs via Tesseract.js, entirely in your browser — your receipt images are never uploaded. The recognition engine's code and language data are fetched from a CDN, so OCR needs an internet connection (typically each time, not just the first, since those specific helper files aren't cached for offline use the way the rest of the app is). Vendor/amount/date extraction is heuristic (regex-based) — always double-check before saving.
- **PDF Export**: real downloadable PDFs (via jsPDF) for invoices and every report, not just a browser print dialog.
- **Audit Trail**: hooks into the app's single storage layer, so every create/update/delete across every module is captured automatically. Capped at the last 500 events per business.
- **Service Worker**: network-first for HTML, cache-first for assets. Cache name: `ledgeros-v5.0`.

---

## Browser Support

Works best in current versions of Chrome or Edge (required for Sync's File System Access API); Firefox and Safari support everything else but not the Sync feature.

Requires a modern browser with localStorage and ES6+ support.

---

## Roadmap Ideas (not yet implemented)

- Deeper multi-currency (bills and expenses, not just invoices)
- Bank feed auto-import (currently CSV only)
- A real backend for true real-time multi-user collaboration
- Per-field audit history (old value → new value, not just "updated")
- Inventory lot/serial tracking, barcode scanning

---

## License

Use freely for personal or commercial projects. Attribution appreciated but not required.

---

**LedgerOS** — beautiful books, zero cloud dependency.
