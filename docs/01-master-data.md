# 01 – Master Data

Clean master data is the foundation of P2P. Most P2P errors (wrong price, wrong G/L account, missing source) trace back here.

## 1. Material Master

| Item | Detail |
|------|--------|
| T-codes | `MM01` create · `MM02` change · `MM03` display · `MM60` material list |
| Fiori | *Manage Product Master Data* |
| Key tables | `MARA` (general) · `MARC` (plant) · `MARD` (storage location) · `MBEW` (valuation) · `MAKT` (description) |

**Views used in P2P**

| View | Key fields for P2P |
|------|-------------------|
| Basic Data | Base unit of measure, material group |
| Purchasing | Purchasing group, order unit, GR processing time |
| MRP 1–4 | MRP type, lot size, reorder point, planned delivery time |
| Accounting 1 | **Valuation class** (drives G/L account), price control `S`/`V`, standard/moving price |
| Plant data / Storage | Storage location, batch management |

> **Tip:** Price control `S` (standard price) creates price-difference postings (PRD) at GR/IR; price control `V` (moving average) absorbs differences into stock value where stock is available.

## 2. Supplier Master (Business Partner)

| | SAP ECC | SAP S/4HANA |
|--|---------|-------------|
| Create | `XK01` / `MK01` / `FK01` | **`BP`** (role `FLVN00` FI vendor, `FLVN01` purchasing) |
| Tables | `LFA1`, `LFB1`, `LFM1` | `BUT000` + `LFA1`, `LFB1`, `LFM1` (kept via CVI) |
| Fiori | – | *Manage Business Partner Master Data* |

**Customer-Vendor Integration (CVI)** synchronizes BP with the classic vendor tables. In S/4HANA, `XK01` etc. redirect to `BP`.

Key supplier data for P2P:
- **Company code level:** reconciliation account, payment terms, payment methods
- **Purchasing org level:** order currency, Incoterms, GR-based invoice verification flag, partner functions

## 3. Purchasing Info Record

Stores the price and conditions for a **material + supplier** combination.

| Item | Detail |
|------|--------|
| T-codes | `ME11` / `ME12` / `ME13` |
| Fiori | *Manage Purchasing Info Records* |
| Tables | `EINA` (general) · `EINE` (purch. org) · conditions in `A017`/`A018` + `KONP` |
| Categories | Standard · Subcontracting · Pipeline · Consignment |

Info records default the price into the PO and are updated automatically when the *Info update* indicator is set on the PO item.

## 4. Source List & Quota Arrangement

| Object | T-code | Purpose |
|--------|--------|---------|
| Source list | `ME01` | Allowed/fixed/blocked suppliers per material & plant (`EORD`) |
| Quota arrangement | `MEQ1` | Split requirements across suppliers by % (`EQUK`, `EQUP`) |
| Fiori | *Manage Sources of Supply* | |

Source list can be made mandatory per plant in config (*Source list requirement at plant level*).

## Configuration Checklist

- [ ] Material types & number ranges (`OMS2`)
- [ ] Valuation classes & account category references (`OMSK`)
- [ ] BP roles, groupings and CVI mapping
- [ ] Partner functions for suppliers
- [ ] Source list requirement per plant
