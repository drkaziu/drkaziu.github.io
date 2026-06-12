---
layout: post
title: "The Database Landscape: A Field Guide"
date: 2026-06-11
categories: [data-engineering]
tags: [databases, sql, postgresql, redis, mongodb, clickhouse]
description: "What actually makes PostgreSQL, Redis, MongoDB, ClickHouse and friends different — explained through the trade-offs each one makes, with a concrete example for every database."
---

Databases differ mainly in three things: **what shape of data they store**, **what questions they're optimized to answer fast**, and **what guarantees they make** (consistency vs speed vs scale). Everything else follows from those trade-offs. This is a field guide to the main families, with one concrete example each.

## 1. PostgreSQL — the general-purpose relational workhorse

**Shape:** Tables with rows and columns, strict schema, relationships enforced via foreign keys. ACID transactions — a transfer of money either fully happens or fully doesn't.

**Use when:** You're building almost anything — web apps, internal tools, analytics-lite. It's the sane default. It also has surprisingly good JSON support, so it covers many "NoSQL" cases too.

```sql
CREATE TABLE trades (
    id            SERIAL PRIMARY KEY,
    market        TEXT NOT NULL,
    delivery_hour TIMESTAMPTZ NOT NULL,
    price_eur     NUMERIC(8,2),
    volume_mwh    NUMERIC(10,3),
    meta          JSONB  -- flexible extras without schema changes
);

-- Average hourly price, classic relational strength
SELECT date_trunc('hour', delivery_hour) AS h,
       AVG(price_eur)
FROM trades
WHERE market = 'NordPool'
GROUP BY h ORDER BY h;
```

**Personality:** Open source, standards-compliant, extensible (PostGIS for geo, TimescaleDB for time series). If you only learn one database deeply, learn this one.

## 2. MySQL / MariaDB — Postgres's pragmatic sibling

**Shape:** Same relational model. Historically simpler and faster for read-heavy web workloads; historically looser about correctness (silent data truncation in old versions).

**Use when:** Classic web stacks (WordPress, many PHP and legacy systems), read-heavy apps with simple queries. The differences from Postgres today are mostly ecosystem and operational habits, not capability.

```sql
-- Identical-looking SQL; the differences are under the hood
SELECT user_id, COUNT(*) AS orders
FROM orders
WHERE created_at >= NOW() - INTERVAL 30 DAY
GROUP BY user_id;
```

**Rule of thumb:** new project → Postgres; joining a team that runs MySQL → MySQL is fine.

## 3. Microsoft SQL Server — the enterprise relational database

**Shape:** Relational, ACID, same family as Postgres and MySQL — but commercial, deeply integrated with the Microsoft ecosystem (Windows Server, .NET, Power BI, Azure, Excel connectivity).

**Use when:** You're in a corporate environment that runs on Microsoft. Its dialect is **T-SQL**, which has some distinctive syntax:

```sql
-- T-SQL flavor: TOP instead of LIMIT, square brackets, GETDATE()
SELECT TOP 10 [market], AVG([price_eur]) AS avg_price
FROM [dbo].[trades]
WHERE [delivery_hour] >= DATEADD(day, -7, GETDATE())
GROUP BY [market]
ORDER BY avg_price DESC;
```

**Personality:** Excellent tooling (SQL Server Management Studio), strong stored-procedure culture, licensing costs money. You'll likely meet this in energy and finance companies — it's everywhere in that world.

## 4. SQLite — the database that's just a file

**Shape:** Relational SQL, but the entire database is a single file on disk. No server, no network, no users — your program opens the file directly.

**Use when:** Mobile apps, desktop apps, embedded devices, prototypes, local analysis. It's the most deployed database on Earth — it's in your phone, your browser, your car.

```python
import sqlite3

con = sqlite3.connect("prices.db")   # creates the file if missing
con.execute("CREATE TABLE IF NOT EXISTS p (hour TEXT, eur REAL)")
con.execute("INSERT INTO p VALUES ('2026-06-11T14:00', 87.50)")
```

**Anti-use:** Many concurrent writers from different machines. It's a file, not a server.

## 5. MongoDB — documents instead of tables

**Shape:** Stores JSON-like **documents** in collections. No fixed schema — each document can have different fields. Nested structures live inside one record instead of being split across joined tables.

**Use when:** Your data is naturally hierarchical and self-contained (a product with variants, a user profile with settings), or the schema evolves quickly in early development.

```javascript
db.bids.insertOne({
  market: "NordPool",
  hour: ISODate("2026-06-11T14:00Z"),
  blocks: [                       // nested array — would need a separate
    { price: 85.0, volume: 10 },  // table + join in SQL
    { price: 92.5, volume: 5 }
  ]
});

db.bids.find({ "blocks.price": { $gt: 90 } });
```

**Trade-off:** You give up joins and strict consistency guarantees in exchange for flexibility. The classic failure mode is using Mongo for inherently relational data and reinventing joins in application code, badly.

## 6. Redis — everything lives in RAM

**Shape:** Key-value store held in memory. Values aren't just strings — they can be lists, sets, sorted sets, hashes. Microsecond latency.

**Use when:** Caching, sessions, rate limiting, leaderboards, queues, pub/sub. Redis is almost never your *primary* database — it sits in front of one, absorbing reads.

```bash
SET session:kazimieras '{"role":"analyst"}' EX 3600   # expires in 1h
GET session:kazimieras

# Sorted set = instant leaderboard / price ranking
ZADD spot_prices 87.5 "LT" 91.2 "LV" 84.0 "EE"
ZREVRANGE spot_prices 0 2 WITHSCORES   # top 3, highest first
```

**Trade-off:** RAM is expensive and volatile. Persistence exists but is secondary; treat Redis data as rebuildable.

## 7. Elasticsearch — built for search, not storage

**Shape:** Documents indexed into an **inverted index** — like the index at the back of a book, mapping every word to where it appears. That's why full-text search over millions of documents returns in milliseconds.

**Use when:** Search bars (typo-tolerant, relevance-ranked), log analysis (the ELK stack), filtering products by many facets.

```json
POST /articles/_search
{
  "query": {
    "match": { "body": { "query": "electricty price", "fuzziness": "AUTO" } }
  }
}
```

That `fuzziness` finds "electricity" despite the typo — something `WHERE body LIKE '%electricty%'` in SQL could never do, and the LIKE would be catastrophically slow anyway.

**Trade-off:** Not a source of truth. Data gets copied *into* Elasticsearch from a real database.

## 8. ClickHouse (and DuckDB) — columnar analytics

**Shape:** Stores data by **column** instead of by row. When you compute `AVG(price)` over a billion rows, it reads only the price column from disk — not entire rows — and compresses similar values brutally well. This is the OLAP (analytics) family, vs OLTP (transactions) like Postgres.

**Use when:** Aggregations over huge datasets — years of hourly market data, scanned and grouped in seconds.

```sql
-- ClickHouse: this over 5 billion rows finishes in ~1 second
SELECT toStartOfMonth(delivery_hour) AS m,
       avg(price_eur), quantile(0.95)(price_eur)
FROM nordpool_prices
GROUP BY m;
```

**DuckDB** is the same idea but embedded like SQLite — a single-file analytics engine that queries Parquet and CSV files directly:

```python
import duckdb

duckdb.sql("SELECT market, avg(price) FROM 'prices_*.parquet' GROUP BY market")
```

**Trade-off:** Terrible at updating individual rows. You append and aggregate; you don't run a banking app on it.

## 9. Cassandra — write-heavy, planet-scale

**Shape:** Wide-column store distributed across many machines with no single master. Designed so any node can fail and the cluster keeps accepting writes. The catch: you must know your queries *in advance* and design tables around them — no flexible ad-hoc joins.

**Use when:** Massive write throughput across data centers — IoT sensor floods, messaging at Discord or Netflix scale.

```sql
-- CQL looks like SQL, but the PRIMARY KEY *is* the query plan:
-- partition by sensor, sort by time → "give me sensor X's recent readings"
CREATE TABLE readings (
  sensor_id UUID,
  ts        TIMESTAMP,
  value     DOUBLE,
  PRIMARY KEY (sensor_id, ts)
) WITH CLUSTERING ORDER BY (ts DESC);
```

**Trade-off:** Eventual consistency — two nodes may briefly disagree on the latest value. Fine for sensor data, unacceptable for account balances.

## Summary table

| Database | Model | Optimized for | Killer feature | Avoid for |
|---|---|---|---|---|
| PostgreSQL | Relational | Everything general-purpose | Correctness + extensibility | Extreme scale-out writes |
| MySQL | Relational | Read-heavy web apps | Ubiquity, simplicity | — (same as PG, roughly) |
| SQL Server | Relational | Enterprise / Microsoft shops | Tooling, BI integration | Budget projects (licensing) |
| SQLite | Relational, embedded | Local / single-app data | Zero setup, one file | Concurrent multi-user writes |
| MongoDB | Document (JSON) | Flexible, nested data | Schema freedom | Highly relational data |
| Redis | In-memory key-value | Sub-millisecond reads | Data structures in RAM | Primary / durable storage |
| Elasticsearch | Inverted index | Full-text search, logs | Fuzzy, ranked search | Source of truth |
| ClickHouse / DuckDB | Columnar | Aggregations over billions of rows | Analytical speed | Row-level updates |
| Cassandra | Wide-column, distributed | Massive write volume | No single point of failure | Strong consistency needs |

## Closing thought

A realistic production system often uses several of these at once: Postgres as source of truth, Redis caching hot reads, Elasticsearch powering the search bar, ClickHouse holding the analytics history. Picking a database is less "which is best" and more "which trade-off matches this workload."
