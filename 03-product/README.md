# Product Specifications — Simple Stock Flow

This document details the product capabilities, functional scope, and user personas for Simple Stock Flow.

---

## 1. Product Vision & Value Proposition

Simple Stock Flow is designed as a streamlined, high-reliability inventory and point-of-sale reporting solution. It minimizes operational overhead by enforcing strict data invariants (such as non-negative stock and immutable historical transaction snapshots) directly within the domain and persistence layers.

---

## 2. User Personas

| Persona | Role | Core Goals | Key Interactions |
|---|---|---|---|
| **Store Administrator** | `admin` | Maintain product catalog, manage store seller accounts, and analyze aggregated sales performance. | Product CRUD, user provisioning, sales report generation. |
| **Sales Clerk** | `seller` | Efficiently process multi-item customer purchases with accurate real-time inventory adjustments. | Stock lookup, sales transaction creation. |

---

## 3. Core Functional Capabilities

### Catalog Management
* Add new products with name, price, initial stock, category, and optional image reference key.
* Update existing product details (price, stock adjustments, category assignment).
* Perform soft deletion (`deleted_at`) on products to preserve historical reporting integrity.

### Sales Processing
* Register multi-item sales transactions in a single operation.
* Automatically deduct inventory stock per line item with optimistic concurrency control (`xmin`).
* Snapshot product attributes (`unit_price`, `product_name`, `category_name`) at the exact moment of sale to guarantee historical immutability.

### Sales Reporting
* Generate aggregated sales reports over customizable date ranges.
* Group sales metrics by product and frozen category names.
