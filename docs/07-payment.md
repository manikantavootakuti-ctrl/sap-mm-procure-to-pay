# 07 – Payment

After invoice posting, the supplier open item sits in FI-AP until it is paid. Payment is owned by **FI**, but MM consultants must understand it for end-to-end testing and issue analysis.

## Transactions & Apps

| Action | ECC / GUI | S/4HANA Fiori |
|--------|-----------|---------------|
| Automatic payment run | `F110` | *Manage Automatic Payments* |
| Manual outgoing payment | `F-53` / `F-58` (with print) | *Post Outgoing Payments* |
| Supplier line items | `FBL1N` | *Manage Supplier Line Items* |
| Supplier balances | `FK10N` | *Display Supplier Balances* |

## F110 Steps

1. **Parameters** – run date, identification, company codes, payment methods, next posting date, suppliers
2. **Proposal** – system selects due items (respecting payment blocks, e.g. `R` from LIV)
3. **Edit proposal** – review exceptions
4. **Payment run** – posts payment documents
5. **Printout / DME** – payment medium (e.g. SEPA XML)

## Accounting Entry

| Dr/Cr | Account |
|-------|---------|
| Dr | Supplier (clears open item) |
| Cr | Bank / bank clearing |
| Cr | Cash discount received (if taken) |

## What MM Influences

| MM / master data | Effect on payment |
|------------------|-------------------|
| Payment terms (BP / PO) | Due date & cash discount |
| Invoice blocks from LIV | Item excluded from F110 until released |
| Supplier bank details (BP) | Where money is paid |
| Partner functions (invoicing party) | Who gets paid |

## Full P2P Document Trail

Use **PO history** (`ME23N` → *Purchase Order History* tab, table `EKBE`) to trace GR and invoice documents, then `FBL1N` / *Manage Supplier Line Items* for the clearing (payment) document.
