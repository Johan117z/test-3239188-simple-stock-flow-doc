# Requirements — Simple Stock Flow

## Functional Requirements
- **FR-01**: Catalog CRUD operations supporting soft deletion (`deleted_at`).
- **FR-02**: Sales transaction recording with price and category data freezing.
- **FR-03**: Sales performance reports aggregated by product within date ranges.

## Non-Functional Requirements
- **NFR-01**: Database engine must run PostgreSQL 16.14 in UTC timezone.
- **NFR-02**: Financial attributes use 2 decimal places (`numeric(18,2)`).
- **NFR-03**: Concurrency control enforced via PostgreSQL `xmin` token.
