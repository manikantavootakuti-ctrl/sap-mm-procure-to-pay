# 05 - Goods receipt

GR against the PO. For stock items this increases stock quantity and value, and you get two documents: a material document and an accounting document.

## T-codes / apps

- MIGO - action A01 (goods receipt), reference R01 (purchase order). Fiori: *Post Goods Receipt for Purchasing Document*
- MB03 or MIGO to display. Fiori: *Material Documents Overview*
- MMBE / MB52 for stock. Fiori: *Stock - Single Material*, *Stock - Multiple Materials*
- MBST or cancel in MIGO

In S/4 the old MB01, MB1A, MB1B, MB1C, MB31 etc. are gone. Everything goes through MIGO.

## Movement types I use most

| mvt | what |
|---|---|
| 101 | GR for PO (into unrestricted, QI or blocked) |
| 102 | reversal of 101 |
| 103 | GR into GR blocked stock - not valuated yet |
| 105 | release from GR blocked stock -> now valuated |
| 122 | return to supplier |
| 161 | GR for a returns PO item |
| 351 / 101 | STO - issue from one plant, receipt in the other |

103/105 is useful when goods arrive but need checking before you accept them into stock.

## Stock types

- unrestricted
- quality inspection - QM active, or stock type set on the PO item
- blocked - damaged / disputed
- GR blocked (103) - received, not accepted, not valuated

## Tables - this is where S/4 is really different

ECC: MKPF (header) + MSEG (item), plus a bunch of aggregate stock tables (MARD, MCHB...).

S/4: everything is in MATDOC. MKPF and MSEG still exist as compatibility views so old reports don't break, and stock is calculated from MATDOC on the fly.

Accounting: BKPF / BSEG in ECC, BKPF / ACDOCA in S/4.

## Posting (stock item, price control V)

Dr inventory (BSX) / Cr GR/IR (WRX)

With price control S, if the PO price isn't equal to the standard price, the difference goes to PRD.

For account-assigned items (e.g. K, cost center) the debit goes to the consumption account instead of inventory.

## Errors you'll see

- "Posting only possible in periods ..." -> MM period not open. MMPV to close/open, OMSY to check.
- "Account determination for entry ... not possible" -> missing OBYC entry for that valuation class / key.
- over delivery error -> tolerance on PO item too low, or tick unlimited.
