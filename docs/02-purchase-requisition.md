# 02 - Purchase requisition

A PR is just an internal request - "we need this". It doesn't go to the supplier and doesn't post anything in FI.

## Where PRs come from

- manual entry - ME51N or the Fiori app *Create Purchase Requisition*
- MRP - MD01N (MRP Live) in S/4, MD01/MD02 in ECC
- PM / PS orders for non-stock components
- self-service / catalog requests

## T-codes

| What | GUI | Fiori |
|---|---|---|
| create | ME51N | Create Purchase Requisition |
| change / display | ME52N / ME53N | Manage Purchase Requisitions |
| release one | ME54N | My Inbox (flexible workflow) |
| release many | ME55 | My Inbox |
| list | ME5A | Monitor Purchase Requisition Items |
| assign source + convert | ME57 | Manage Purchase Requisitions - Professional |

Tables: EBAN (items), EBKN (account assignment).

## Fields worth knowing

- doc type - NB is the standard one
- item category - blank = standard, L = subcontracting, K = consignment, U = stock transfer, D = service
- account assignment - blank = stock, K = cost center, F = order, P = project (WBS), A = asset
- desired / fixed supplier, valuation price

## Release strategy (classic)

This is the classification-based one. Steps roughly:

1. characteristics in CT04, e.g. CEBAN_GSWRT (total value), CEBAN_WERKS (plant)
2. class with class type 032 in CL02
3. release groups, codes, indicators, strategies in SPRO: MM > Purchasing > Purchase Requisition > Release Procedure > Procedure with Classification
4. maintain the values in the classification tab of the strategy

Release indicator X = blocked, 2 = released (RFQ/PO can be created).

In S/4 SAP recommends flexible workflow instead (configured in the Fiori app *Manage Workflows for Purchase Requisitions*). The classic strategy still works though, and plenty of brownfield systems keep it.

## Things I check when a PR "doesn't work"

- PR won't convert to PO -> is it released? is there a source assigned?
- release strategy not triggering -> characteristic values don't match, or the class isn't assigned to the release group
- MRP not creating PRs -> procurement type is E (in-house) instead of F, or MRP type is wrong
