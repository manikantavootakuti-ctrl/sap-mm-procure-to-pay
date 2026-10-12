# 01 - Master data

Honestly most P2P issues I've looked at end up being master data issues. Wrong price on the PO? Check the info record. Wrong G/L on the GR? Check the valuation class. So this comes first.

## Material master

MM01 / MM02 / MM03. In Fiori it's *Manage Product Master Data*.

Tables you'll end up in: MARA (general), MARC (plant), MARD (storage location), MBEW (valuation), MAKT (description).

Views that matter for purchasing:

- Basic data - base UoM, material group
- Purchasing - purchasing group, order unit, GR processing time
- MRP 1-4 - MRP type, lot size, planned delivery time
- Accounting 1 - valuation class and price control. This one decides which G/L account the GR posts to, so get it right.

Price control S vs V is worth understanding properly. With S (standard price) any difference between PO price and standard price goes to the price difference account (PRD). With V (moving average) the difference goes into the stock value instead, as long as there's stock to absorb it.

## Supplier = Business Partner (in S/4)

In ECC you had XK01 / MK01 / FK01. In S/4HANA it's all transaction BP. The old T-codes just redirect you to BP.

Roles you need for a normal supplier:
- FLVN00 - FI vendor (company code data)
- FLVN01 - supplier for purchasing (purch. org data)

The classic tables LFA1, LFB1, LFM1 still exist and are kept in sync through CVI (customer-vendor integration). BP general data sits in BUT000.

What matters from the supplier for P2P:
- company code level: reconciliation account, payment terms, payment methods
- purch. org level: order currency, incoterms, GR-based IV flag, partner functions

## Info record

ME11 / ME12 / ME13. Price and conditions for one material + supplier combo.

Tables: EINA (general), EINE (purch. org level). Condition records via A017/A018 and KONP.

Types: standard, subcontracting, pipeline, consignment.

The PO picks up the price from here. If "info update" is ticked on the PO item, the info record gets updated from the PO - handy, but it also means a typo on a PO can quietly change the info record.

## Source list and quota arrangement

- Source list - ME01, table EORD. Which suppliers are allowed / fixed / blocked for a material in a plant. You can make it mandatory per plant in config.
- Quota arrangement - MEQ1 (EQUK, EQUP). Splits demand across suppliers by percentage.

Fiori: *Manage Sources of Supply* covers both.

## Config I usually check

- material types and number ranges (OMS2)
- valuation classes / account category reference (OMSK)
- BP roles, groupings, CVI number range mapping
- partner functions for suppliers
- source list requirement per plant
