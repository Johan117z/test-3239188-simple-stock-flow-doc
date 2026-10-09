# Architectural Decision Records Log

---

### ADR-001: Schema Ownership via EF Core Migrations

* **Status**: Accepted
* **Date**: 2026-09-19

#### Context
The database schema must be version-controlled, reproducible, and deterministic across development, testing, and production environments. Manual DDL execution creates schema drift and unverified environments.

#### Decision
All Data Definition Language (DDL) changes in the PostgreSQL database are exclusively managed through Entity Framework Core Migrations. Manual DDL scripts or direct table modifications in database engines are strictly prohibited.

#### Consequences
* **Positive**: Fully automated schema versioning and deterministic CI/CD pipeline deployments.
* **Negative**: All database changes require an EF Core migration generation step.

---

### ADR-002: Optimistic Concurrency Control & Stock Validation

* **Status**: Accepted
* **Date**: 2026-09-19

#### Context
High-frequency concurrent sales transactions can attempt to withdraw stock simultaneously, leading to race conditions and negative inventory levels.

#### Decision
Implement Optimistic Concurrency Control using the PostgreSQL native `xmin` system column mapped as a shadow token in EF Core. Combine this with a PostgreSQL database constraint `ck_product_stock_non_negative` (`CHECK (stock >= 0)`).

#### Consequences
* **Positive**: Prevents row-level database locks, ensures high throughput, and guarantees that stock never drops below zero at the engine level.
* **Negative**: Concurrent updates on the same product require application retry handling upon concurrency exceptions.

---

### ADR-003: Soft Deletion Strategy for Catalog Items

* **Status**: Accepted
* **Date**: 2026-09-19

#### Context
Product records are referenced historically by sales transactions. Physical deletion (`DELETE`) would orphan sales line items or break aggregate sales reports.

#### Decision
Products utilize a soft deletion pattern via a `deleted_at` nullable timestamp column combined with EF Core Global Query Filters (`deleted_at IS NULL`). Physical `DELETE` operations on products are disabled.

#### Consequences
* **Positive**: Preserves historical integrity for reports while removing deleted items from active catalog queries.
* **Negative**: Unique name indexes on products must be partial (`WHERE deleted_at IS NULL`) to allow re-creating products with previously deleted names.

---

### ADR-004: Data Freezing on Sales Line Items

* **Status**: Accepted
* **Date**: 2026-09-19

#### Context
Products and categories can be renamed or re-priced over time. Historical sales reports must reflect the exact terms and prices at the moment a purchase was made, rather than live catalog data.

#### Decision
Every line item (`sale_item`) explicitly copies and freezes `product_name`, `category_name`, and `unit_price` at the exact moment of sale creation.

#### Consequences
* **Positive**: Historical sales records remain immutable and accurate even if the underlying product or category is updated or soft-deleted.
* **Negative**: Requires storing duplicate strings in `sale_item` records at transaction time.
