# System Context — Simple Stock Flow

This document defines the high-level system boundaries, key actors, external integrations, and architectural scope for Simple Stock Flow.

---

## 1. System Overview

Simple Stock Flow is an internal inventory and sales management system. It enables store operators to manage product catalog items, maintain real-time inventory counts, process sales transactions with frozen historical pricing, and generate aggregated sales reports.

---

## 2. Actors & Roles

The system strictly serves internal store operators. No external customer or buyer entity exists within the system boundaries.

* **Admin (`admin`)**: Responsible for managing the product catalog (create, update, soft delete), managing store seller accounts, and reviewing sales reports.
* **Seller (`seller`)**: Responsible for querying available catalog stock and registering multi-item sales transactions.

---

## 3. System Boundaries & External Integrations

* **Relational Persistence**: PostgreSQL 16.14 engine running in UTC. Enforces relational integrity, check constraints, and optimistic concurrency control (`xmin`).
* **External Image Storage**: Object/blob storage service holding product image binaries. Referenced exclusively through opaque string keys (`image_key`).
* **Application API**: ASP.NET Core REST API serving input ports and enforcing business rules.

---

## 4. Scope Boundaries

### In Scope
* Catalog management with soft deletion (`deleted_at`).
* Real-time stock decrement and non-negative stock enforcement (`stock >= 0`).
* Immutable sales transaction recording with frozen snapshot attributes (`unit_price`, `product_name`, `category_name`).
* Dynamic sales aggregation reports grouped by product within date ranges.

### Out of Scope
* Customer/buyer entity or loyalty program management.
* Multi-currency processing (the system is strictly single-currency).
* External payment gateway integration.
