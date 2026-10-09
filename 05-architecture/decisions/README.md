# Architecture — Simple Stock Flow

## 1. Architectural Style

The system is built following **Hexagonal Architecture** (Ports and Adapters), ensuring the domain core remains completely independent of infrastructure concerns such as PostgreSQL 16.14 persistence or web transport frameworks.

## 2. Aggregates & Entities (§2)

- **Product** (Catalog Aggregate Root): Manages item attributes (`name`, `price`, `stock`, `category_id`, `image_key`).
- **Sale & SaleItem** (Sales Aggregate Root & Internal Entity): Represents immutable commercial transactions where lines freeze historical data.
- **User** (Identity Aggregate Root): Manages internal operators with roles restricted to `admin` or `seller`.
- **Category** (Reference Entity): Fixed set of 5 read-only seed classifications.

## 3. System Ports

- **Read Model Port for Sales Reports**: Aggregation by product over a date range calculated directly in the engine via a read port (**D-06**).
- **Hashing Port**: The domain never sees plain-text passwords; credential hashing is produced exclusively via an outbound port (**D-09**).
- **Storage Port**: External binary management handled via opaque string keys (`image_key`) (**D-08**).

## 4. Rule Enforcement Locations (§4)

- **Engine (PostgreSQL)**: Primary keys, unique indexes (`IX_category_name`, `IX_user_username`), foreign keys (**FK-1**, **FK-2**, **FK-3**), and the stock non-negative check constraint (`ck_product_stock_non_negative`).
- **Domain-Only (C#)**: Invariants like `price > 0`, `quantity > 0`, username normalization, and process rules.
- **Pending (Tasks T-xx)**: Constraints and features scheduled in `tasks.md`, such as **T-20** (lowering remaining domain-only checks to the engine), **T-11** (frozen category name), **T-12** (`sold_by_user_id`), and **T-13** (performance indexes).
