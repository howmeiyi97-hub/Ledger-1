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

Ledger is one self-contained file, `index.html`. Open it in a browser, or host it on any static site host (GitHub Pages, Netlify, Vercel).

Outside the Claude app, a few things work differently:

- Data is saved in your browser's local storage, not synced across devices.
- Receipt scanning, file downloads and cloud sync are turned off. These use Claude's artifact features.

It loads two libraries from cdnjs: `qrcode-generator` for the PayNow QR code and `jsPDF` for invoice PDFs.
