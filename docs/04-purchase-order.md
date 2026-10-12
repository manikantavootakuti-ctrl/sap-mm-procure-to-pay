# 04 - Purchase order

The PO is the document everything else hangs off. GR and invoice both reference it, and the PO history tells you the whole story.

## T-codes / apps

- ME21N create, ME22N change, ME23N display. Fiori: *Create Purchase Order - Advanced*, *Manage Purchase Orders*
- ME59N - auto-create POs from PRs
- ME29N (single) / ME28 (collective) - release
- reports: ME2N (by PO number), ME2L (by supplier), ME2M (by material), ME80FN (general). Fiori: *Monitor Purchase Order Items*
- ME9F - output

## Tables

- EKKO - header
- EKPO - item
- EKET - schedule lines
- EKKN - account assignment
- EKBE - PO history (every GR and invoice against the item). This is the one I end up in most.
- PRCD_ELEMENTS - pricing conditions in S/4. In ECC it was KONV.

## Item level controls that cause confusion

- GR indicator - goods receipt expected
- GR non-valuated - GR is quantity only, no posting. Typical for account-assigned items.
- IR indicator - invoice expected
- GR-based IV - invoice has to be matched to specific GRs, not just the PO line
- confirmation control - needs an order acknowledgement / inbound delivery
- over/under delivery tolerance - % deviation allowed at GR

## Pricing procedure

Schema group of the purch. org + schema group of the supplier -> pricing procedure (standard one is RM0000).

Common conditions: PB00 gross price, RA01 discount %, FRB1 freight, SKTO cash discount.

## Output

ECC used NAST / message determination (NACE) with SAPscript or Smart Forms.

S/4 uses the BRF+ based output management (Output Parameter Determination) and Adobe forms. If you're migrating, plan time for the PO form - it always takes longer than expected.

## Release strategy

Works the same way as for PRs, just with characteristics on CEKKO (e.g. CEKKO_GNETW for net value, CEKKO_EKORG). Release status is in EKKO-FRGKE. A PO that isn't released can't be output.
