# 09 - ECC vs S/4HANA, what changes for MM

ECC 6.0 mainstream maintenance ends in 2027 (extended maintenance until 2030 for those who pay for it), so most ECC customers are either planning or already in their S/4 move. These are the MM-relevant changes I think you really need to know.

## Main differences

| | ECC | S/4HANA |
|---|---|---|
| supplier master | XK01 / MK01 / FK01 | BP, with CVI. CVI has to be done before the conversion. |
| material docs | MKPF + MSEG + aggregate tables | MATDOC. Custom reports on the old aggregates need checking. |
| inventory T-codes | MB01, MB1A, MB1B, MB1C, MB31... | MIGO only |
| accounting | BSEG, COEP, FAGLFLEXA... | ACDOCA (universal journal) |
| material number | 18 chars | up to 40 chars (optional) - watch interfaces |
| MRP | MD01 / MD02 | MRP Live, MD01N |
| pricing table | KONV | PRCD_ELEMENTS |
| output | NAST / NACE | BRF+ output management |
| approvals | classic release strategy | flexible workflow recommended (classic still works) |
| UI | SAP GUI | Fiori + GUI |
| supplier evaluation | ME61 etc. | Supplier Evaluation apps in Fiori |

## Checklist for an MM workstream

- run the simplification item check / readiness check, go through the MM items
- CVI - every vendor must end up as a BP
- clean up before cutover: old open POs, old PRs, GR/IR balances
- custom ABAP reading MSEG, aggregate stock tables or KONV
- decide: keep classic release strategy or move to flexible workflow
- PO / RFQ forms for the new output management
- Fiori roles for buyers, warehouse, AP
- for greenfield: migration objects in the Migration Cockpit - materials, suppliers, info records, source lists, open POs, stock balances

## Approaches

- greenfield - new system, only master data and open items come over
- brownfield - convert the existing ECC system, history and config stay
- selective / "bluefield" - somewhere in between, selective data transition
