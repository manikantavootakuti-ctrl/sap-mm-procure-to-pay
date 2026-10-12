# 06 - Invoice verification (LIV)

The supplier invoice gets checked against the PO (price, terms) and the GR (quantity). That's the 3-way match everyone talks about.

If it's within tolerance it posts and becomes an open item for payment. If not, it still posts but gets a payment block, and someone has to release it later.

## T-codes / apps

- MIRO - enter invoice. Fiori: *Create Supplier Invoice*
- MIR7 - park
- MIR4 - display. Fiori: *Manage Supplier Invoices*
- MRBR - release blocked invoices
- MR8M - cancel
- MR11 - GR/IR account maintenance
- MRRL - ERS (evaluated receipt settlement, i.e. no supplier invoice, SAP creates it from the GR)

Tables: RBKP (header), RSEG (item), RBCO (account assignment).

## Posting

- Dr GR/IR (WRX)
- Dr input tax (VST)
- Dr/Cr price difference if any - PRD with price control S, or BSX with V when there's stock coverage
- Cr supplier (recon account from BP)

## Tolerances (OMR6)

The ones I see configured on almost every project:

- PP - price variance
- DQ - quantity variance (invoice qty vs GR qty)
- DW - quantity variance when nothing has been received yet
- PS - price variance on estimated prices
- ST - date variance
- BD - small differences, posted automatically
- BR / BS - percentage OPUn variance
- AN / AP - amount limits for items without / with order reference

## Why is my invoice blocked?

Blocking reasons on the item:

- R - price
- M - quantity
- D - date
- I - quality inspection
- S - stochastic (random) block
- or someone blocked it manually

The supplier line item gets payment block R, so F110 skips it. MRBR releases it - either manually, or automatically once the reason is gone (e.g. the missing GR got posted).

## GR/IR

Open GR/IR balances build up when GR and invoice never fully match - supplier won't send the last invoice, quantity was short shipped and nobody cleaned up, etc. MR11 clears them. Worth checking every month end, auditors always ask about it.
