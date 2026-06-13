# observa_streamhouse

A change data capture (CDC) pipeline that streams data changes from PostgreSQL to object storage, with full observability built in.

## Overview

`observa_streamhouse` captures row-level changes from PostgreSQL's write-ahead log (WAL), streams them through Kafka, and lands them in S3-compatible object storage. Every stage is monitored end to end, with metrics and logs collected by Prometheus and visualized in Grafana.

The pipeline runs on artificially generated data — starting with a financial use case such as stock price tracking.

## Flow

```
PostgreSQL (WAL) → Debezium → Kafka → S3 Sink Connector → MinIO
                          ↓
                  Prometheus → Grafana
```

## Stack

- **PostgreSQL** — source database (logical replication via WAL)
- **Debezium** — CDC connector + UI
- **Kafka & Kafka Connect** — streaming backbone, with a UI for inspection
- **S3 Sink Connector + MinIO** — final landing zone (mock S3)
- **Prometheus** — metrics and log collection across all components
- **Grafana** — dashboards, organized per tool
- **Python** — synthetic data generation

## Monitoring

Metrics are captured from Debezium, PostgreSQL, Kafka, and Kafka Connect, then surfaced in Grafana dashboards grouped by category. Logs are collected through Prometheus, with a log-querying tool planned for a later stage.

## Status

Active and evolving. The data domain and scope will expand over time.

