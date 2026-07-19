---
title: Caching Strategies
updated: 2026-07-10T12:52:39+07:00
tags:
  - cache
  - system-design
---

There are several [[cache|caching]] strategies:

- Refresh Ahead
- Write-Behind
- Write-through
- Cache Aside

## Refresh Ahead

**Example:** Product catalog pages, trending news feeds, session metadata, or dashboard widgets.

```mermaid
sequenceDiagram
    participant Client
    participant Cache
    participant Source as Data Source

    Client->>Cache: Read data
    Cache-->>Client: Return cached data
    Note over Cache: Entry is close to expiring
    Cache->>Source: Refresh in background
    Source-->>Cache: Return current data
    Cache->>Cache: Replace cached entry
```

## Write-Behind

**Example:** Logging, analytics event ingestion, like counters, activity tracking, or telemetry buffers.


```mermaid
sequenceDiagram
    participant Client
    participant Cache
    participant Source as Data Source

    Client->>Cache: Write data
    Cache-->>Client: Acknowledge immediately
    Note over Cache,Source: Asynchronous write
    Cache->>Source: Persist queued update
    Source-->>Cache: Confirm persistence
```

## Write-Through

**Example:** User profiles, inventory counts, banking balances, order status.

```mermaid
sequenceDiagram
    participant Client
    participant Cache
    participant Source as Data Source

    Client->>Cache: Write data
    Cache->>Source: Persist data
    Source-->>Cache: Confirm persistence
    Cache->>Cache: Update cached entry
    Cache-->>Client: Acknowledge write
```

## Cache Aside

**Example:** User profiles, blog posts, configuration data, search results, or API responses.

```mermaid
sequenceDiagram
    participant Client
    participant App as Application
    participant Cache
    participant Source as Data Source

    Client->>App: Request data
    App->>Cache: Look up data
    alt Cache hit
        Cache-->>App: Return cached data
    else Cache miss
        Cache-->>App: Not found
        App->>Source: Query data
        Source-->>App: Return data
        App->>Cache: Store data
    end
    App-->>Client: Return data
```
