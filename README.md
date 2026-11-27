# Orders & Dispatch (CALGAS Capacitors)

Customer orders, the batches made for them, receiving finished batches into
stores, and dispatches with a printable delivery note. This is the rebuilt
Production Tracker (4.0); the repository took the app's own name on
27 Nov 2026 (it was calgas/Production-Tracker). Same sign-in.

https://calgas.github.io/Orders-Dispatch/

## How the three apps fit together

1. **Orders & Dispatch** — Marketing or Dispatch enters the customer order:
   one or more items, each made in one or more batches.
2. **Batch Card Tracker** — each batch is opened for an order line ("Open
   batch" on the order or the Plan page fills it in), recorded stage by stage
   with PQA, and its serial numbers are entered at Testing & Packing.
3. **Orders & Dispatch → Stores** — a batch that passed Final Audit is
   received into stores. Stock Management books it into FG stock (reference:
   the batch number).
4. **Orders & Dispatch → Dispatch** — the goods go out against the order:
   the order's own batches first, then batches made for stock, oldest first,
   and their serial numbers follow. The delivery note prints (or saves as a
   PDF) in three copies. Stock Management books the goods out of FG stock.

Stock moves are never posted from this app directly: it records the receipt or
dispatch, then asks Stock Management to post it, which reads the record and
writes the ledger entry back. Asking twice posts once.

## Access

Signed in with the Stock Management account (app `pt`). An Admin gives or
removes access in Stock Management → Team & Access → Orders & Dispatch:

| Feature | What it allows |
|---|---|
| See orders, plan, stores and dispatches | Read everything |
| Do your department's work | What the department has in Settings → Each department's work (Marketing and Dispatch: orders and customers; Stores: receiving; Dispatch: dispatches) |
| Enter and edit orders | Orders, for any department |
| Add and edit customers | The customer list |
| Receive finished batches into stores | Stores receipts |
| Make and print dispatches | Dispatches and delivery notes |
| Cancel a dispatch or undo a receipt | Takes the stock back |

Company details on the delivery note (address, GSTIN, prefixes, declaration)
are under Settings (Admins).

## Files

`index.html` is built from `production-tracker/web/` in the private
`calgas/apps-backend` repository (`build.py`); `sw.js` keeps the app shell for
offline starts — bump `CACHE_VERSION` with every release.
