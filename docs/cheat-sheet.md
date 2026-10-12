# SAP MM P2P – Cheat Sheet

## Transaction Codes

| Step | Create | Change | Display | Other |
|------|--------|--------|---------|-------|
| Material | `MM01` | `MM02` | `MM03` | `MM60` list · `MMBE` stock |
| Supplier (S/4) | `BP` | `BP` | `BP` | `XK03` (redirects) |
| Info record | `ME11` | `ME12` | `ME13` | `ME1L` list |
| Source list | `ME01` | `ME01` | `ME03` | `ME0M` list |
| Purchase requisition | `ME51N` | `ME52N` | `ME53N` | `ME54N` / `ME55` release · `ME5A` list · `ME57` assign |
| RFQ | `ME41` | `ME42` | `ME43` | `ME4L` list |
| Quotation | `ME47` | `ME47` | `ME48` | `ME49` price comparison |
| Purchase order | `ME21N` | `ME22N` | `ME23N` | `ME29N`/`ME28` release · `ME2N`/`ME2L`/`ME2M`/`ME80FN` reports · `ME59N` auto-PO |
| Contract | `ME31K` | `ME32K` | `ME33K` | `ME3L` list |
| Scheduling agreement | `ME31L` | `ME32L` | `ME33L` | `ME38` delivery schedule |
| Goods receipt | `MIGO` | – | `MB03` / `MIGO` | `MB51` material doc list · `MB52` warehouse stock · `MBST` cancel |
| Invoice | `MIRO` | `MIR7` park | `MIR4` | `MRBR` release · `MR8M` cancel · `MR11` GR/IR · `MRRL` ERS |
| Payment | `F110` | – | `FBL1N` | `F-53` manual payment |

## Key Tables

| Object | Tables |
|--------|--------|
| Material | `MARA`, `MARC`, `MARD`, `MBEW`, `MAKT` |
| Supplier | `BUT000`, `LFA1`, `LFB1`, `LFM1` |
| Info record | `EINA`, `EINE` |
| Source list | `EORD` |
| Purchase requisition | `EBAN`, `EBKN` |
| Purchasing documents | `EKKO`, `EKPO`, `EKET`, `EKKN`, `EKBE` |
| Pricing | `PRCD_ELEMENTS` (S/4) / `KONV` (ECC) |
| Material document | `MATDOC` (S/4) / `MKPF`, `MSEG` (ECC) |
| Invoice | `RBKP`, `RSEG` |
| Accounting | `BKPF`, `ACDOCA` (S/4) / `BSEG` |

## Movement Types

`101` GR · `102` GR reversal · `103` GR blocked · `105` release GR blocked · `122` return to supplier · `201` GI cost center · `261` GI order · `301` plant-to-plant · `311` sloc-to-sloc · `551` scrapping · `561` initial stock

## Config T-codes

`OMS2` material types · `OMSK` valuation classes · `OMWD` valuation grouping · `OBYC` account determination · `OMR6` invoice tolerances · `OMSY` / `MMPV` MM periods · `OMJJ` movement types · `SPRO` IMG
