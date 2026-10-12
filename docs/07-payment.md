# 07 - Payment

Strictly speaking this is FI territory, not MM. But when you test P2P end to end you need to get the invoice paid, and a lot of "why wasn't the supplier paid" questions end up back with MM anyway. So here's the minimum.

## T-codes / apps

- F110 - automatic payment run. Fiori: *Manage Automatic Payments*
- F-53 manual outgoing payment (F-58 with print)
- FBL1N - supplier line items. Fiori: *Manage Supplier Line Items*
- FK10N - supplier balances

## F110 in short

1. parameters - run date, ID, company codes, payment methods, next posting date, suppliers
2. proposal - SAP picks the due items (skips anything with a payment block)
3. check / edit the proposal
4. payment run - posts the payment docs
5. print / DME file (SEPA XML in Europe)

## Posting

Dr supplier (clears the open item) / Cr bank or bank clearing. Plus cash discount if it was taken.

## Where MM affects payment

- payment terms (from BP or the PO) -> due date and discount
- invoice blocked in LIV -> not paid until released in MRBR
- bank details on the BP -> where the money goes
- invoicing party partner function -> who gets paid

## Following the trail

ME23N -> PO history tab (that's EKBE) shows the GR and invoice docs. From the invoice you go to FBL1N to find the clearing document = the payment.
