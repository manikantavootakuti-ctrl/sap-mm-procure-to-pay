# 05 – Goods Receipt (GR)

Posting the receipt of goods against the PO. For stock material this **increases inventory quantity and value** and creates both a **material document** and an **accounting document**.

## Transactions & Apps

| Action | ECC / GUI | S/4HANA Fiori |
|--------|-----------|---------------|
| Post GR | `MIGO` (A01 Goods Receipt / R01 Purchase Order) | *Post Goods Receipt for Purchasing Document* |
| Display material doc | `MB03` / `MIGO` | *Material Documents Overview* |
| Stock overview | `MMBE` · `MB52` | *Stock – Single Material* · *Stock – Multiple Materials* |
| Cancel | `MBST` / `MIGO` (cancellation) | *Material Documents Overview* |

> In S/4HANA the old `MB01`, `MB1A`, `MB1B`, `MB1C`, `MB31` etc. are **obsolete** – use `MIGO`.

## Key Movement Types

| Mvt | Description | Stock effect |
|-----|-------------|--------------|
| `101` | GR for PO into unrestricted / QI / blocked | + stock (valuated) |
| `102` | Reversal of 101 | − stock |
| `103` | GR into **GR blocked stock** (not valuated) | No valuated stock |
| `105` | Release from GR blocked stock to warehouse | + stock (valuated) |
| `122` | Return delivery to supplier | − stock |
| `161` | Return PO item (returns indicator) | − stock |
| `351` / `101` | Stock transport order: GI / GR | Transfer between plants |

## Stock Types

- **Unrestricted** – available for use
- **Quality inspection** – if QM active or *Stock type* = `X` on PO
- **Blocked** – damaged / disputed goods
- **GR blocked** (`103`) – received but not yet accepted, not valuated

## Tables

| | ECC | S/4HANA |
|--|-----|---------|
| Material document | `MKPF` (header), `MSEG` (item) | **`MATDOC`** (single table; `MKPF`/`MSEG` remain as compatibility views) |
| Stock quantities | `MARD`, `MCHB`, aggregate tables | Calculated on the fly from `MATDOC` |
| Accounting | `BKPF` / `BSEG` | `BKPF` / **`ACDOCA`** |

## Accounting Entry (stock material, price control V)

| Dr/Cr | Account | Transaction key |
|-------|---------|-----------------|
| Dr | Inventory | `BSX` |
| Cr | GR/IR clearing | `WRX` |

If price control is `S` and PO price ≠ standard price → difference to **`PRD`** (price difference).

For **consumption** items (account assignment `K` cost center), the debit goes to the consumption account via `GBB`/`VBR` or directly to the account from the PO's account assignment.

## Common Issues

| Error | Fix |
|-------|-----|
| *Posting only possible in periods…* | Open MM period with `MMPV` / check `OMSY` |
| *Account determination for entry … not possible* | Missing `OBYC` entry for the valuation class |
| Overdelivery error | Increase overdelivery tolerance on PO / set unlimited flag |
