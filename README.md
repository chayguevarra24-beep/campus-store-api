# Campus Store API Design Document

* **Student Name:** Joyce Anne J. Guevarra
* **Section:** ACT2
* **Activity:** Week 5 — Design a Campus Store API

---

## 1. Endpoints & Pagination

This section covers retrieving products, filtering/sorting the catalog, and placing orders.

### API Endpoints
* **Get Single Product:** `GET /api/v1/products/{id}`
* **List Products:** `GET /api/v1/products`
* **Create Order:** `GET /api/v1/orders`

### Pagination Choice: Cursor-Based Pagination
For a campus store with thousands of products, **cursor-based pagination** (using a `cursor` and `limit` parameter) is chosen over offset-based pagination (`page` & `offset`). Offset pagination causes performance degradation on large database tables (`OFFSET 10000` scans 10,000 rows) and misses/duplicates items if new products are added while browsing. Cursors point to a stable reference (like `id` or timestamp).

### Example Requests & Responses

**First Request (Initial page load):**
```http
GET /api/v1/products?limit=2&category=stationery&sort=price_asc
