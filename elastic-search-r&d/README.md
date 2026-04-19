# Search Infrastructure R&D — Zero-Downtime Reindex

A production SaaS platform was experiencing downtime every time a search index schema change was needed. The assumption was that the search engine itself was the problem. This R&D effort evaluated alternatives, diagnosed the real cause, and resolved it without migrating to any new infrastructure.

## Problem

The existing platform used Elasticsearch (AWS OpenSearch managed clusters) for event search. Every time a schema change was required — adding a new filterable field, changing a mapping — it triggered a full reindex that took production down for its duration. There was no rollback path if the reindex failed mid-run.

## Evaluation

Four alternatives were evaluated across pricing, geo search, typo tolerance, alias-swap support, auto-scaling, and operational overhead:

| Option | Outcome |
|---|---|
| Algolia | Dropped — unpredictable cost at scale |
| Typesense | Capable, but new infrastructure and cost without justification |
| AWS OpenSearch Serverless | Dropped — $525/mo floor unjustified at current scale |
| Elastic Cloud Serverless | Dropped — new infrastructure, existing clusters sufficient |

## Diagnosis

The downtime was not caused by the search engine. It was caused by the reindex implementation — no alias management, no automated rollover, manual steps in the AWS console, and no resume path if the process failed halfway through.

OpenSearch has supported alias-swap reindexing since version 1.0. The existing clusters already had everything needed. The fix was an implementation change, not a platform migration.

## What Was Built

A zero-downtime reindex pipeline inside a NestJS microservice:

- **Drift detection on every deployment** — compares the mapping defined in code against the live index on startup; triggers a background reindex automatically if drift is found
- **Alias-swap pattern** — builds the new index version in the background while the old index stays live; swaps atomically on completion
- **Cursor-based resume** — all reindex state is persisted in MySQL; if the service crashes mid-job, it resumes from the exact row it stopped at on restart
- **Phase-aware crash recovery** — handles crashes at any phase (backfill, alias swap, cleanup) with the correct recovery action per phase
- **Isolated DB connection pool** — reindex batch queries use a separate Prisma client with a hard connection limit so they cannot starve the live query path
- **Scheduled reindex** — triggered via AWS EventBridge → Lambda on a 3-hour interval; the endpoint is idempotent and handles concurrent job guards internally

## Architecture

- **search-service** — dedicated NestJS microservice; owns the OpenSearch client, index mappings, and both indexing and search query logic
- Domain services publish RabbitMQ messages on data changes; search-service consumes and upserts documents
- api-service routes GraphQL queries to search-service via RabbitMQ RPC
- Zero database hits on the read path — all data is denormalized into the search document at index time

## Technology

AWS OpenSearch (managed clusters), NestJS, RabbitMQ, Prisma, MySQL, AWS EventBridge, AWS Lambda, AWS App Runner

## Outcome

Zero additional infrastructure cost. Zero migration risk. Zero downtime on schema changes going forward. The reindex that previously required manual AWS console steps and took production offline now runs entirely in the background, resumes automatically after failures, and requires no manual intervention.
