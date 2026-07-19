---
title: Cache invalidation
updated: 2026-07-10T16:23:38+07:00
tags:
  - system-design
  - cache
---


Cache invalidation removes or updates cached data when its source changes. It is needed when waiting for the TTL to expire would leave data stale for too long.


- **Delete on write:** update the database, then delete the related cache key. The next read repopulates it.
- **Update on write:** update the database and cached value together, as in write-through caching.
- **Event-driven invalidation:** publish an event when data changes so services or CDN edges can invalidate affected entries.
- **Versioned keys:** include a version in the key or URL, such as `product:42:v3` or `app.a1b2c3.js`, so new data uses a new cache entry.
- **Manual purge:** explicitly clear selected keys or paths when content is published or corrected.

# Time to Live (TTL)

A **TTL** defines how long a cached entry remains valid. When the TTL expires, the cache removes the entry or treats it as a miss so fresh data can be fetched from the source.:

- Use a short TTL for frequently changing data.
- Use a long TTL for stable data, such as country lists or versioned static assets.
- Add random variation, or **TTL jitter**, to prevent many keys from expiring simultaneously and causing a [[cache-stampede|cache stampede]].
- A TTL limits staleness but does not guarantee that the cache always contains the latest value.
