# Project Governance — Simple Stock Flow

This document defines the governing standards for development, version control, naming conventions, and contribution workflows within the repository.

---

## 1. Version Control & Branching Strategy

The repository follows **Trunk-Based Development**:
* **Primary Branch**: `main` represents the stable, production-ready baseline.
* **Feature Branches**: Work must be conducted in short-lived topic branches (e.g., `feature/T-02-initial-schema`, `fix/T-10-stock-check`) and merged via Pull Requests.
* **Direct Commits**: Restricted to `main` except for initial repository setup and documentation hotfixes.

---

## 2. Commit Message Standards

Commits must strictly comply with **Conventional Commits**:

| Type | Description | Example |
|---|---|---|
| `feat:` | Adding a new domain capability, aggregate, or endpoint | `feat: implement product soft delete filter` |
| `fix:` | Correcting a bug, constraint failure, or invariant | `fix: enforce non-negative check on product stock` |
| `docs:` | Creating or updating documentation or ADRs | `docs: populate governance guidelines in 00-governance` |
| `chore:` | Maintenance tasks, EF Core migrations, or Docker updates | `chore: generate EF Core initial schema migration` |

---

## 3. Naming Conventions

Standardization across domain code, persistence mappings, and database artifacts:

| Element | Convention | Scope | Example |
|---|---|---|---|
| Domain Entity | `PascalCase`, English, Singular, ASCII | C# Code | `SaleItem` |
| Database Table | `snake_case`, English, Singular, ASCII | PostgreSQL Schema (`sales`) | `sale_item` |
| Database Attribute | `snake_case`, English, Singular, ASCII | PostgreSQL Columns | `unit_price` |
| List Attribute | **Never plural** | PostgreSQL Columns | `sale_item` |
| Domain Collections | `PascalCase`, English, Plural | C# In-Memory Sets | `DbSet<Product> Products` |

---

## 4. Engineering Standards

* **Language**: All code, persistence configuration, API documentation, and commit messages must be written strictly in **English**.
* **Encoding**: All files must be saved using **UTF-8** encoding.
* **Single Source of Truth**: Schema definitions and invariants declared in `spec/data-model.md` are non-negotiable.
