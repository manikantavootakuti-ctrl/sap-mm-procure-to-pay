# 03 - RFQ and quotation

Only needed when there's no fixed source or you want competing quotes. In a lot of companies this step is skipped completely or done outside SAP (Ariba, email...).

## Classic flow

PR -> RFQ (ME41) to each supplier -> enter their quotes (ME47) -> compare (ME49) -> accept the best one, reject the rest -> create PO with reference to the quotation.

In classic MM you get one RFQ per supplier. They're grouped together by a collective number (SUBMI) so ME49 can compare them.

## T-codes / apps

- create RFQ: ME41 / *Manage RFQs*
- maintain quotation: ME47 / *Manage Supplier Quotations*
- price comparison: ME49 / *Compare Supplier Quotations*
- rejection letters: ME4S or via output

## Where it's stored

Same tables as POs - EKKO / EKPO. The document category (EKKO-BSTYP) tells you what it is:

- A = RFQ / quotation
- F = purchase order
- K = contract
- L = scheduling agreement

Good to remember when writing queries on EKKO - always filter on BSTYP.

## Notes

- In S/4 the newer RFQ object can be sent to Ariba Sourcing / Ariba Network for supplier collaboration.
- Accepted quote prices can update the info record (info update flag in ME47).
