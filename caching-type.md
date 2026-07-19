---
title: Caching Type
updated: 2026-07-10T16:10:00+07:00
tags:
  - system-design
  - cache
---

[[cache|Caching]] can happen at several layers. Using multiple layers reduces latency and prevents every request from reaching the origin database or service.

## Client-side caching

Stores data on the user's device, so repeated access is fast and network usage is reduced. Best for static assets and limited offline use.

**Examples:**

- **Browser cache:** stores HTML, CSS, JavaScript, images, and fonts.
- **Application cache:** stores API responses, user profile data, and preferences.

**Risk:** the server cannot immediately remove every client copy, so versioned asset names and appropriate expiration times are important.

## Application caching

The server application caches objects that are expensive to retrieve or compute.

- **Local in-memory cache:** very fast, but not shared between instances and lost when the process restarts.
- **Distributed cache:** stored in systems such as Redis or Memcached; shared by multiple application instances.
  - Suitable for sessions, API results, database records, and computed values.

**Risk:** [[cache-stampede|cache stampede]]

## Web server and reverse-proxy caching

A web server or reverse proxy, such as Nginx or Varnish, caches complete HTTP responses near the application server. Useful for pages or API responses requested by many users.

- Can store HTML, API responses, and RSS feeds.
- Reduces work on the origin server by serving repeated requests directly from cache.

## Database caching

This can occur inside the DBMS/database engine, storing frequently used database data or results in memory so the database can answer faster.

- **Buffer/page cache:** keeps disk pages in RAM.
- **Query/result cache:** saves repeated query outputs.
- **Materialized views:** store precomputed query results.
- **Read replicas:** reduce load by serving reads, though they are not true caches.
- **Execution plan cache:** reuses query plans for repeated statements in some databases.

## DNS caching

Stores domain name lookup results so the same hostname does not need to be resolved repeatedly.

- Can happen in the browser, operating system, local router, recursive resolver, or CDN edge resolver.
- Uses a TTL to decide how long a DNS record should be kept.
- If a DNS record changes, cached results may stay visible until the TTL expires.
- Helps reduce latency before the connection starts, because the client gets the server IP faster.

## [[content-delivery-network-cache|CDN caching]]

A CDN stores static assets and cacheable responses at geographically distributed edge locations.

- Reduces latency by serving content from a location close to the user.
- Reduces bandwidth and request load on the origin server.
- Commonly caches images, videos, scripts, stylesheets, downloads, and sometimes public API responses.
- Content is refreshed through expiration, revalidation, versioned URLs, or explicit cache purging.
