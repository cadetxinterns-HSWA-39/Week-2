# Sprint Notes — Week 2

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

**Sprint scope:** Data Integration & Dataset Merging, Feature Engineering for Analytics

## What was completed

- Built two integration structures — a lean fact/dimension split and a fully denormalized set of joined views — and verified both produce consistent, row-accurate results.
- Confirmed `inventory_position.csv` carries forward the `scale_mismatch_flag` from Week 1's cleaning findings rather than dropping the issue.
- Built the Feature Engineering outputs: delivery lead time, payment window, and PO lead variance features on the two transaction-level tables, plus a new `customer_features.csv` RFM table.
- Carried the `invoice_id_ambiguous` flag from Week 1 into `sales_transactions.csv`, since that table pulls in `invoice_id` and would otherwise inherit the same collision risk silently.

## Decisions made

- Kept both integration structures rather than standardising on one, since each is used for a different purpose — the lean tables for analytical work, the denormalized views for BI.
- Held off on a stockout or reorder-point feature this week, since the `current_stock` vs. threshold scale mismatch from Week 1 is still unresolved at the source. Used stock_ledger-derived velocity instead, where needed.

## Corrections after review

`customer_features.csv` originally labelled GST-inclusive revenue as plain `total_revenue`. It now has separate `_incl_gst` and `_ex_gst` columns (22,958,987,430 ex-GST; 29,253,993,162 incl-GST), and the Feature Engineering log was updated to match.

## Next steps

Week 3: Data Validation & Consistency Checks, Data Dictionary & Documentation, KPI framework.
