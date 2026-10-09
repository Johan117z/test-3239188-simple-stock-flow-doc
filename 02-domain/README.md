# Domain Model — Simple Stock Flow

## 1. Core Domain Aggregates
- **Product Aggregate**: Handles product catalog details (`Product`, `Money`, `Quantity`, `Category`).
- **Sale Aggregate**: Encapsulates immutable transaction records (`Sale` root and `SaleItem` entities).
- **User Aggregate**: Manages operator credentials and roles (`User`, `Role`).

## 2. Key Business Invariants
- Inventory levels cannot drop below zero (`stock >= 0`).
- Line items snapshot product attributes (`unit_price`, `product_name`, `category_name`) at sale time.
- Completed sales are strictly immutable and cannot be updated or physically deleted.
