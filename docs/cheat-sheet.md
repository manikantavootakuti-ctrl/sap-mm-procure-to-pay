# Cheat sheet

The stuff I look up most often.

## T-codes

| | create | change | display | other |
|---|---|---|---|---|
| material | MM01 | MM02 | MM03 | MM60 list, MMBE stock |
| supplier (S/4) | BP | BP | BP | XK03 just redirects to BP |
| info record | ME11 | ME12 | ME13 | ME1L list |
| source list | ME01 | ME01 | ME03 | ME0M list |
| PR | ME51N | ME52N | ME53N | ME54N/ME55 release, ME5A list, ME57 assign |
| RFQ | ME41 | ME42 | ME43 | ME4L list |
| quotation | ME47 | ME47 | ME48 | ME49 price comparison |
| PO | ME21N | ME22N | ME23N | ME29N/ME28 release, ME2N/ME2L/ME2M/ME80FN, ME59N |
| contract | ME31K | ME32K | ME33K | ME3L list |
| sched. agreement | ME31L | ME32L | ME33L | ME38 delivery schedule |
| GR | MIGO | - | MB03 / MIGO | MB51 doc list, MB52 stock, MBST cancel |
| invoice | MIRO | MIR7 (park) | MIR4 | MRBR, MR8M, MR11, MRRL |
| payment | F110 | - | FBL1N | F-53 |

## Tables

- material: MARA, MARC, MARD, MBEW, MAKT
- supplier: BUT000, LFA1, LFB1, LFM1
- info record: EINA, EINE
- source list: EORD
- PR: EBAN, EBKN
- purchasing docs: EKKO, EKPO, EKET, EKKN, EKBE
- pricing: PRCD_ELEMENTS (S/4), KONV (ECC)
- material docs: MATDOC (S/4), MKPF + MSEG (ECC)
- invoice: RBKP, RSEG
- accounting: BKPF, ACDOCA (S/4), BSEG

## Movement types

101 GR, 102 reversal, 103 GR blocked, 105 release from GR blocked, 122 return to supplier, 201 GI to cost center, 261 GI to order, 301 plant to plant, 311 sloc to sloc, 551 scrapping, 561 initial stock

## Config

OMS2 material types, OMSK valuation classes, OMWD valuation grouping, OBYC account determination, OMR6 invoice tolerances, OMSY / MMPV periods, OMJJ movement types
