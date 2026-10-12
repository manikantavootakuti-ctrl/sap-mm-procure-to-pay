# 09 – SAP ECC vs S/4HANA: What Changes for MM

SAP ECC 6.0 mainstream maintenance ends in **2027** (optional extended maintenance to 2030), so most ECC customers are planning or running their S/4HANA migration. These are the changes an MM consultant must know.

## Simplification Items – Summary

| Area | SAP ECC | SAP S/4HANA | Impact |
|------|---------|-------------|--------|
| Supplier master | `XK01`/`MK01`/`FK01` | **Business Partner** (`BP`) with CVI | CVI conversion is a mandatory pre-step for migration |
| Material documents | `MKPF` + `MSEG` + aggregate tables | **`MATDOC`** single table | Custom reports reading aggregates must be checked |
| Inventory transactions | `MB01`, `MB1A`, `MB1B`, `MB1C`, `MB31`… | **`MIGO`** only | Retrain users |
| Accounting | `BSEG`, `COEP`, `FAGLFLEXA`… | **`ACDOCA`** (Universal Journal) | Real-time MM–FI–CO reconciliation |
| Material number | 18 characters | **40 characters** (extended, optional) | Interfaces & custom code |
| MRP | `MD01` / `MD02` classic | **MRP Live** (`MD01N`) | HANA-optimized, faster planning |
| Pricing table | `KONV` | **`PRCD_ELEMENTS`** | Custom code reading `KONV` |
| Output management | NAST / `NACE` | **BRF+ output management** | New config & forms |
| Approvals | Classic release strategy | **Flexible workflow** (recommended) | Configured in Fiori |
| UI | SAP GUI | **SAP Fiori** apps + GUI | Role-based launchpad design |
| Supplier evaluation | `ME61` etc. | *Supplier Evaluation* Fiori apps | Analytics embedded |

## Migration Readiness Checklist (MM)

- [ ] Run **Simplification Item Check** / Readiness Check, review MM items
- [ ] Complete **CVI** – every vendor must map to a BP
- [ ] Clean up open POs, old PRs and GR/IR balances before cut-over
- [ ] Review custom ABAP using `MSEG`, aggregate stock tables, `KONV`
- [ ] Decide classic release strategy vs flexible workflow
- [ ] Redesign PO and RFQ output forms
- [ ] Define Fiori roles/catalogs for buyers, warehouse clerks, AP clerks
- [ ] Data migration objects in **SAP S/4HANA Migration Cockpit** (new implementations): materials, suppliers (BP), info records, source lists, open POs, inventory balances

## Migration Approaches

| Approach | Description |
|----------|-------------|
| **Greenfield** | New implementation, migrate master data & open items only |
| **Brownfield** | System conversion of existing ECC (keeps history & config) |
| **Selective / Bluefield** | Selective data transition – mix of both |
