# Domain Model — Simple Stock Flow

This document defines the core domain aggregates, entities, value objects, and business invariants governing the application.

---

## 1. Domain Aggregates & Entities

### Product (Catalog Aggregate Root)
* **Entity**: `Product`
* **Responsibility**: Manages product catalog attributes including name, unit price, available stock, category assignment, and optional image key.
* **Key Operations**: `Rename`, `ChangePrice`, `Withdraw`, `Restock`, `SetCategory`, `AttachImage`.

### Sale (Sales Aggregate Root)
* **Entities**: `Sale` (Root), `SaleItem` (Internal Line Item Entity)
* **Responsibility**: Encapsulates immutable sales transactions.
* **Key Behavior**: Adding a line item (`Sale.AddItem`) enforces stock withdrawal (`Product.Withdraw`) in a single operation. Once registered, a sale cannot be updated or deleted.

### User (Identity Aggregate Root)
* **Entity**: `User`
* **Responsibility**: Manages internal operator identity and role privileges (`admin`, `seller`).
* **Key Behavior**: Enforces username normalization to lowercase and protects plain-text passwords through domain ports.

### Category (Reference Entity)
* **Entity**: `Category`
* **Responsibility**: Read-only classification reference. Contains a fixed set of 5 seed categories initialized via migrations.

---

## 2. Value Objects

* **`Money`**: Encapsulates monetary values using 2 decimal places (`MidpointRounding.AwayFromZero`). Designed for a single-currency system without storing currency codes.
* **`Quantity`**: Represents sold unit counts, enforcing `quantity > 0`.

---

## 3. Fundamental Business Invariants

1. **Non-Negative Inventory**: Inventory levels must never drop below zero (`stock >= 0`).
2. **Data Freezing on Sale Items**: `SaleItem` creates immutable snapshots of `product_name`, `category_name`, and `unit_price` at the moment of sale.
3. **Soft Deletion**: Products use `deleted_at` timestamps for removal, preventing physical database deletions.
4. **Single Currency**: System operates exclusively in one currency; no currency attributes are stored in tables.
5. **Username Uniqueness**: Operator usernames are trimmed, normalized to lowercase, and unique across the system.
