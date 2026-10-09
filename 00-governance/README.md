# Project Governance — Simple Stock Flow

## 1. Branching Strategy
This repository follows **Trunk-Based Development**.
- Short-lived feature branches are created for specific tasks.
- All code is reviewed and merged into `main`.

## 2. Commit Standards
Commits strictly adhere to **Conventional Commits**:
- `feat:` New business capability or domain logic.
- `fix:` Bug fixes or constraint updates.
- `docs:` Documentation changes across repository sections.
- `chore:` Maintenance, configuration, Docker, or build tooling updates.

## 3. Language Conventions
- **Code & Specs**: Written strictly in **English**.
- **Database Naming**: Entities in `PascalCase` singular (C#); tables in `snake_case` singular (PostgreSQL schema `sales`).
