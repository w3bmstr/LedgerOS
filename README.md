# LedgerOS v3.0

**Complete privacy-first bookkeeping software** for freelancers and small businesses.

Runs entirely in your browser. No accounts, no cloud, no tracking. All data stays on your device until you choose to export it.

![LedgerOS](https://img.shields.io/badge/version-3.0-c9963a) ![PWA](https://img.shields.io/badge/PWA-ready-2eb87a) ![Offline](https://img.shields.io/badge/offline-first-3b7ef6)

---

## Features

### Sales
- **Clients** — contact management
- **Estimates / Quotes** — create, send status, convert to invoice in one click
- **Invoices** — line items, tax, due dates, status (draft / pending / paid / overdue), PDF-style view

### Purchases
- **Vendors** — supplier directory
- **Bills (Accounts Payable)** — track what you owe, due dates, mark paid
- **Expenses** — categorized, recurring flag, vendor tracking

### Accounting
- **Chart of Accounts** — standard small-business CoA (Assets, Liabilities, Equity, Income, Expenses)
- **Journal Entries** — double-entry (debits = credits), automatic balance updates
- **Reports**
  - Profit & Loss
  - Balance Sheet
  - Trial Balance
  - Sales by Client
  - Tax Summary (estimated)
  - Accounts Receivable Aging

### People
- **Employees** — role, pay type (salary / hourly), rate, status
- **Payroll** — bi-weekly pay runs with gross / estimated tax / net, history & YTD

### Planning
- **Budgets** — Business mode + Personal mode with separate categories
- **Spreadsheet** — lightweight grid with `=SUM()`, `=AVG()`, `=COUNT()`, `=MAX()`, `=MIN()`, cell references, CSV export

### System
- Dark / light mode
- Global search (⌘/Ctrl + K)
- Keyboard shortcuts (`?` for help)
- Full JSON backup / restore
- Installable PWA + offline support
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

3. On first load you’ll see sample data and an onboarding modal.
4. Go to **Settings** → update your business name, tax rate, currency, etc.

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

- All data is stored in **localStorage** under keys prefixed with `lo2_`.
- Nothing is sent to any server.
- Use **Settings → Export All Data** to download a full JSON backup.
- Use **Settings → Import Data** to restore from a backup.
- **Clear All Data** resets everything to the seeded demo state.

### Backed-up entities
Clients · Invoices · Estimates · Expenses · Vendors · Bills · Chart of Accounts · Journal · Employees · Pay Runs · Budgets · Spreadsheet · Settings

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

## Technical Notes

- **Double-entry**: Journal entries require matching debits and credits. Account balances update automatically.
- **Payroll**: Simplified estimate (flat ~20% deduction). Not a substitute for real payroll software or a CPA.
- **Tax Summary**: Illustrative only — always consult a tax professional.
- **Service Worker**: Network-first for HTML, cache-first for assets. Cache name: `ledgeros-v3.0`.
- **Chart.js** is loaded from CDN for dashboard charts (cached by the service worker when possible).

---

## Browser Support

Works best in current versions of:
- Chrome / Edge
- Firefox
- Safari (desktop & iOS)

Requires a modern browser with localStorage and ES6+ support.

---

## Roadmap Ideas (not yet implemented)

- Multi-line journal entries
- Bank reconciliation
- Fixed assets / depreciation
- Inventory / COGS tracking
- Multi-currency transactions
- Recurring invoice automation
- PDF export of invoices & reports
- Optional backend / multi-user sync

---

## License

Use freely for personal or commercial projects. Attribution appreciated but not required.

---

**LedgerOS** — beautiful books, zero cloud dependency.
