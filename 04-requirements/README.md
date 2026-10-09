# Requirements — Simple Stock Flow

This document details the functional and non-functional requirements governing the Simple Stock Flow backend system.

---

## 1. Functional Requirements (FR)

### Catalog Management
* **FR-01**: The system must allow creating products with a name, positive price, stock, assigned category, and optional image key.
* **FR-02**: The system must allow updating existing product price, stock levels, and category assignments.
* **FR-03**: The system must implement soft deletion for products using a `deleted_at` timestamp. Physical database deletions of products are strictly prohibited.
* **FR-04**: The system must retrieve product listings filtered by partial text, category, and active status (`deleted_at IS NULL`).

### Sales Transactions
* **FR-05**: The system must process multi-item sales transactions in a single operation.
* **FR-06**: The system must automatically decrement product stock upon sale confirmation.
* **FR-07**: The system must freeze `product_name`, `category_name`, and `unit_price` on each `SaleItem` record at the moment of purchase.
* **FR-08**: Registered sales transactions must be strictly immutable; no update or deletion endpoints shall exist for sales.

### Sales Reporting
* **FR-09**: The system must generate aggregated sales performance reports grouped by product within a user-defined date range (`sold_at` in UTC).

### User Authentication & Identity
* **FR-10**: The system must restrict administrative endpoints (`admin` role) and sales creation (`seller` role) using JWT authentication.
* **FR-11**: Username attributes must be trimmed, normalized to lowercase, and guaranteed unique across the system.

---

## 2. Non-Functional Requirements (NFR)

### Data Integrity & Persistence
* **NFR-01**: Database engine must run PostgreSQL 16.14 with the server set to UTC timezone.
* **NFR-02**: Financial monetary attributes (`price`, `unit_price`) must use `numeric(18,2)` with 2 decimal places.
* **NFR-03**: Inventory stock levels must never drop below zero, enforced by database constraint `ck_product_stock_non_negative`.
* **NFR-04**: Concurrency control for stock updates must use PostgreSQL optimistic locking via the `xmin` system token.

### Architecture & Standards
* **NFR-05**: All schema objects must follow singular naming conventions within the `sales` schema.
* **NFR-06**: Schema updates must be managed exclusively through Entity Framework Core Migrations.
