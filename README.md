# CadetX — Heavy Supplier, Inventory & Warehouse Analytics

## Week 2 submission: Data Integration & Dataset Merging + Feature Engineering for Analytics

## Team

- Odetunde Olumide Temitope — Data Scientist
- Kukoyi Zainab Omotola — Data Analyst
- Nyong Asuabiat — Data Analyst

## What's in this folder

```
week-02/
├── Heavy_Suppliers_Warehouse_Merged datasets/
│   ├── sales_fact.csv, purchasing_fact.csv (lean fact tables)
│   ├── products.csv, customers.csv, inventory_master.csv (dimension tables)
│   └── Data Integration_Log.pdf
├── Feature_Engineering_For_Analytics_Log.pdf
├── inventory_position.csv (Integration stage output)
├── sales_transactions.csv (Feature Engineering stage output)
├── purchase_transactions.csv (Feature Engineering stage output)
├── customer_features.csv (Feature Engineering stage output)
├── README.md
└── SPRINT_NOTES_WEEK2.md
```

## 1. Data Integration & Dataset Merging

Two integration structures came out of this stage, both verified against the source line tables with matching row counts on every join — no fan-out, no row loss.

- **Lean fact/dimension split** — `sales_fact.csv`, `purchasing_fact.csv`, plus dimension tables for products, customers, and inventory. Keeps foreign keys only, no repeated dimension data on every row.
- **Denormalized views** — `inventory_position.csv`, and the base structure behind `sales_transactions.csv` / `purchase_transactions.csv`. Everything joined in and ready to pivot directly.

## 2. Feature Engineering for Analytics

- `sales_transactions.csv` — added `order_to_delivery_days`, `order_month`, `order_year`, `invoice_payment_window_days`, and `invoice_id_ambiguous` (flags the 2,555 rows tied to the invoice ID collision from Week 1).
- `purchase_transactions.csv` — added `po_planned_lead_days`, `po_actual_lead_days`, `po_lead_variance_days`.
- `customer_features.csv` — new RFM-style aggregate table, one row per customer, built from Delivered orders only.

## Known limitation carried into Week 3

`inventory_master.current_stock` is still on a different scale than its own threshold fields. `inventory_position.csv` carries a `scale_mismatch_flag` (fires on all 180 rows) in place of a stockout calculation, and no reorder-point logic was attempted this week.
