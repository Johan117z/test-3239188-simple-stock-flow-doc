# System Context — Simple Stock Flow

## 1. Overview
Simple Stock Flow provides a robust backend API for managing store catalog items, inventory levels, and transaction histories.

## 2. System Boundaries & Actors
- **Primary Actors**: Internal store operators (`admin` and `seller`).
- **Storage Engine**: PostgreSQL 16.14 running in UTC.
- **External Storage**: Object Storage service for product binary image blobs.
- **Out of Scope**: Customer identity management, external payment gateway integration, and multi-currency conversions.
