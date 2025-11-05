# Database Interview Refresh

Reinforce relational storage fundamentals so you can articulate trade-offs, indexing strategies, and engine capabilities in interviews.

## Cheat Sheet
- Know when to pick transactional engines (InnoDB, PostgreSQL) vs simpler storage (MyISAM).
- Apply leftmost prefix rules to composite indexes and explain query plan impacts.
- Discuss tooling for diagnosing slow queries (EXPLAIN, slow query logs, monitoring dashboards).

## Quick Refresh
- Compare storage engines (e.g., MyISAM vs InnoDB) with respect to transactions, foreign keys, and indexing.
- Explain how composite indexes work and when additional single-column indexes are still needed.
- Be ready to describe how you diagnose slow queries using `EXPLAIN`, query plans, or monitoring.

## Comparison Snapshot

| Feature / Use Case | MySQL (InnoDB) | PostgreSQL | MongoDB |
| --- | --- | --- | --- |
| **Model** | Relational (row-oriented) | Relational / object-relational | Document (NoSQL) |
| **Transactions** | ACID with MVCC (InnoDB) | ACID with advanced MVCC | Multi-document ACID (v4.0+), best for single-document |
| **Joins & Relationships** | Mature join support, foreign keys | Rich joins, foreign keys, advanced query planner | No joins; use embedded docs or `$lookup` aggregation |
| **Indexes** | B-tree, hash, full-text, spatial (InnoDB) | B-tree, hash, GIN/GiST, BRIN, full-text | B-tree, hashed, geospatial, text |
| **JSON Support** | `JSON` type (binary), good for hybrid workloads | `JSONB` with indexes and operators | Native document model (BSON) |
| **Horizontal Scaling** | Primary-replica; sharding via proxy or Vitess | Primary-replica; sharding via Citus/extension | Native sharding and replica sets |
| **Typical Strengths** | OLTP, read replicas, LAMP stacks | Complex queries, analytics, strict consistency | Flexible schema, rapid iteration, high write scale |
| **Typical Concerns** | Limited parallel query performance, complex sharding | Operational complexity, tuning vacuum/autovacuum | Requires schema governance, eventual consistency defaults |

## Interview Prompts
- **Storage engine selection:** MyISAM supports full-text search but lacks transactions and foreign keys. InnoDB offers ACID guarantees, row-level locking, and FK constraints—why does that matter for OLTP workloads?
- **Composite indexes:** Walk through leftmost prefix rules. Example: With `KEY (name, age, company_name)` you can efficiently query by `name`, `name + age`, or the full composite, but not by `age` alone without another index. Describe how you evaluate index coverage.
- **Normalization vs denormalization:** Outline when you would introduce redundancy for read performance and how you keep data consistent.

## Deep Dive Later
- [Partial index](https://en.wikipedia.org/wiki/Partial_index) for targeted indexes on filtered subsets.
- Review engine-specific documentation (MySQL, PostgreSQL, MongoDB) for features relevant to your upcoming interviews.
