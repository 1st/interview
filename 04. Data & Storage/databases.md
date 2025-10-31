# Database Interview Refresh

Reinforce relational storage fundamentals so you can articulate trade-offs, indexing strategies, and engine capabilities in interviews.

## Quick Refresh
- Compare storage engines (e.g., MyISAM vs InnoDB) with respect to transactions, foreign keys, and indexing.
- Explain how composite indexes work and when additional single-column indexes are still needed.
- Be ready to describe how you diagnose slow queries using `EXPLAIN`, query plans, or monitoring.

## Interview Prompts
- **Storage engine selection:** MyISAM supports full-text search but lacks transactions and foreign keys. InnoDB offers ACID guarantees, row-level locking, and FK constraints—why does that matter for OLTP workloads?
- **Composite indexes:** Walk through leftmost prefix rules. Example: With `KEY (name, age, company_name)` you can efficiently query by `name`, `name + age`, or the full composite, but not by `age` alone without another index. Describe how you evaluate index coverage.
- **Normalization vs denormalization:** Outline when you would introduce redundancy for read performance and how you keep data consistent.

## Deep Dive Later
- [Partial index](https://en.wikipedia.org/wiki/Partial_index) for targeted indexes on filtered subsets.
- Review engine-specific documentation (MySQL, PostgreSQL, MongoDB) for features relevant to your upcoming interviews.
