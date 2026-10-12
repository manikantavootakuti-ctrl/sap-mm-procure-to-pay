# 08 - Account determination (MM-FI)

Every valuated goods movement and every invoice finds its G/L accounts on its own. The config for that is OBYC.

SPRO path: MM > Valuation and Account Assignment > Account Determination > Account Determination Without Wizard.

## How SAP finds the account

It combines:

- chart of accounts (from the company code)
- valuation grouping code (plant -> valuation area -> OMWD)
- transaction key (BSX, WRX, GBB...) - comes from the movement type
- account modifier (VBR, BSA, AUF...) - also from the movement type, only for some keys like GBB
- valuation class (from the material master, Accounting 1 view)

and looks up the G/L account in OBYC.

## Keys you need to know

| key | used for |
|---|---|
| BSX | inventory account |
| WRX | GR/IR clearing |
| GBB | offsetting entry - consumption, scrapping, initial stock etc. (with modifiers VBR, VNG, BSA, AUF...) |
| PRD | price differences |
| KON | consignment liabilities |
| FRL / FRN | subcontracting services |
| UMB | revaluation gain/loss |
| KDM | exchange rate differences |

## Example

Material RM-100, valuation class 3000, price control S, standard price 10.00 EUR.
PO: 100 PC at 10.50 = 1,050.00. Invoice comes in at the same price, 19% VAT.

GR (101):

| | key | account | amount |
|---|---|---|---|
| Dr | BSX | raw material stock | 1,000.00 |
| Dr | PRD | price difference | 50.00 |
| Cr | WRX | GR/IR | 1,050.00 |

Invoice (MIRO):

| | key | account | amount |
|---|---|---|---|
| Dr | WRX | GR/IR | 1,050.00 |
| Dr | VST | input tax | 199.50 |
| Cr | | supplier | 1,249.50 |

If the material had price control V instead, the 50.00 would go to BSX (stock) and the moving average price would go up.

## Related config

- OMWD - group valuation areas
- OMSK - valuation classes, account category reference
- OMWN - account modifiers per movement type
- OBYC - the account determination itself
- OMWB - simulate it (very useful when you're debugging a "no account" error)
