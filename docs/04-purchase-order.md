# 04 – Purchase Order (PO)

A legally binding request to a supplier. The PO is the central document of P2P – GR and invoice both reference it.

## Transactions & Apps

| Action | ECC / GUI | S/4HANA Fiori |
|--------|-----------|---------------|
| Create | `ME21N` | *Create Purchase Order – Advanced* |
| Change / Display | `ME22N` / `ME23N` | *Manage Purchase Orders* |
| Auto-create from PRs | `ME59N` | *Manage Purchase Requisitions – Professional* |
| Release | `ME29N` (individual) · `ME28` (collective) | *My Inbox* (flexible workflow) |
| Reporting | `ME2N` (by number) · `ME2L` (supplier) · `ME2M` (material) · `ME80FN` | *Monitor Purchase Order Items* |
| Output | `ME9F` | *Output Request Items* |

## Key Tables

| Table | Content |
|-------|---------|
| `EKKO` | Header (supplier, purch. org, doc type, currency) |
| `EKPO` | Items (material, qty, price, plant, item category) |
| `EKET` | Schedule lines (delivery dates & quantities) |
| `EKKN` | Account assignment |
| `EKBE` | **PO history** – every GR and invoice against the item |
| `PRCD_ELEMENTS` | Pricing conditions (S/4HANA; `KONV` in ECC) |

## Important Item-Level Controls

| Field | Effect |
|-------|--------|
| **GR indicator** | Goods receipt expected |
| **GR non-valuated** | GR posts quantity only (common with account assignment) |
| **Invoice receipt indicator** | Invoice expected |
| **GR-based IV** | Invoice must be matched to individual GRs |
| **Confirmation control** | Requires order acknowledgment / inbound delivery |
| **Overdelivery / underdelivery tolerance** | Allowed GR deviation in % |

## Pricing Procedure

Determined from: **Schema group of purch. org + schema group of supplier → pricing procedure** (e.g. `RM0000`).

Typical conditions: `PB00` gross price · `RA01` discount % · `FRB1` freight · `SKTO` cash discount.

## Output Management

| | ECC | S/4HANA |
|--|-----|---------|
| Technology | NAST / message determination (`NACE`) | BRF+-based output management (*Output Parameter Determination*) |
| Form | SAPscript / Smart Forms | Adobe Forms / Fiori form templates |

## Release Strategy

Same classification approach as PR, using characteristics on `CEKKO` (e.g. `CEKKO_GNETW` net value, `CEKKO_EKORG`). Release status `EKKO-FRGKE`; PO cannot be output until released.
