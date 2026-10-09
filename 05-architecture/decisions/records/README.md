# Architectural Decision Records (Log)

### ADR-001: Schema Ownership via EF Core Migrations
- **Status**: Accepted
- **Decision**: Database DDL is exclusively managed through EF Core Migrations. Manual DDL scripts in production are strictly forbidden.

### ADR-002: Optimistic Concurrency Control
- **Status**: Accepted
- **Decision**: Concurrency is managed via PostgreSQL `xmin` system column mapped as a shadow token alongside `ck_product_stock_non_negative`.

### ADR-003: Soft Deletion Strategy
- **Status**: Accepted
- **Decision**: Product deletions set a `deleted_at` timestamp. Global query filters prevent physical database deletions to protect historical reports.

### ADR-004: Data Freezing on Sales Line Items
- **Status**: Accepted
- **Decision**: Line items record immutable snapshot copies of product details (`product_name`, `category_name`, `unit_price`) at the moment of sale.
