# Ledger

A personal web app for tracking expenses and sending simple invoices, built for Singapore.

## Features

- **Expenses:** add, edit and search expenses in any currency. Each expense keeps the exchange rate it was saved with, so past totals in SGD never change.
- **Receipt scanning:** take a photo of a receipt and the amount, date, shop and category fill in automatically (needs Claude, inside the Claude app).
- **Smart categories:** the app remembers which category you used for each shop.
- **Design:** light theme with purple accents, smooth animations, and a hamster mascot.
- **Budgets:** a monthly limit per category, with progress bars and alerts at 80% and when you go over.
- **Invoices:** line items, due dates, Draft / Sent / Paid / Overdue status, and a PDF with a PayNow QR code and bank details.
- **Reports:** a monthly summary (highlights, an optional recap written by Claude, and a PDF report), spending by category, the last 6 months, and outstanding invoices.
- **Backup:** export expenses as CSV, or download a full JSON backup and restore it.

## Running it

Ledger is one self-contained file, `index.html`. Host it on any static site host (Vercel, Netlify, GitHub Pages) or open it in a browser.

### Where your data is saved

- **Inside the Claude app:** data syncs to your Claude account. Receipt scanning and Claude recaps work here.
- **Hosted on the web (Vercel etc.):** sign in with email and password (or an emailed sign-in link; "Forgot password?" sends a reset link). Data syncs to the Supabase project `Ledger-1` (`pumgvljnjonbdupqtjec`), and each person can only read and change their own rows (row-level security). The first time you sign in, anything saved in that browser is moved to your account.
- **Offline:** changes made without a connection are saved on the device and upload automatically when you reconnect. Settings shows your account, the sync status, **Sync now** and **Sign out**.
- **Offline or without signing in:** "Use Ledger on this device only" saves to the browser's local storage.

Receipt scanning and Claude recaps need the Claude app, so they're hidden on the hosted version.

### Supabase setup

Tables: `ledger_docs` (expenses, invoices, clients and settings as JSON) and `ledger_receipts` (receipt photos), both with row-level security on `user_id = auth.uid()`.

For email sign-in links to work on a hosted site, add its address in the Supabase dashboard under **Authentication › URL Configuration**: set **Site URL** to your site and add it to **Redirect URLs**.

The publishable key in `index.html` is meant to be public; row-level security protects the data.

It loads `qrcode-generator` and `jsPDF` from cdnjs, and `supabase-js` from jsDelivr.
