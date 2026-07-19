---
title: CDN
updated: 2026-07-10T13:17:36+07:00
tags:
  - system-design
  - cache
---
Content Delivery Network (CDN) is a distributed proxy server that [[cache]] website static content closer to users. This routing visitor requests to the nearest **edge server** rather than the main origin server. CDNs can reduce latency and increase page loading speed, and protect websites from traffic spikes and DDoS attacks

## Pull CDN


```mermaid
sequenceDiagram
    actor User
    participant Edge as CDN Edge
    participant Origin as Origin Server
    User->>Edge: Request asset
    alt Cache hit
        Edge-->>User: Return cached asset
    else Cache miss
        Edge->>Origin: Fetch asset
        Origin-->>Edge: Return asset
        Note over Edge: Cache asset
        Edge-->>User: Return asset
    end
```

- **Advantages:** 
	- simple setup
	- automatic distribution
	- storage only for requested content
- **Trade-offs:** 
	- the first request at each edge location is slower and creates origin traffic
	- stale content may require cache invalidation or versioned URLs.
- **Best for:** websites with large or frequently changing content libraries and unpredictable access patterns.

## Push CDN


```mermaid
sequenceDiagram
    actor Owner as Content Owner
    participant CDN as CDN Storage
    participant Edge as CDN Edge
    actor User
    Owner->>CDN: Upload asset
    CDN->>Edge: Distribute asset
    User->>Edge: Request asset
    Edge-->>User: Return asset
```

- **Advantages:** 
	- no cache-miss request to the origin
	- predictable availability
	- direct control over which files and versions are distributed
- **Trade-offs:** 
	- publishing and invalidation must be managed explicitly
	- unused content may consume CDN storage.
- **Best for:** static and versioned assets, large downloads, software releases, and files that must be available immediately at the edge.
## Comparison

| Aspect             | Pull CDN                          | Push CDN                             |
| ------------------ | --------------------------------- | ------------------------------------ |
| Content transfer   | CDN fetches on demand             | Owner uploads in advance             |
| First request      | May be slower due to a cache miss | Served directly from the CDN         |
| Origin dependency  | Needed on cache misses            | Not needed for delivery after upload |
| Content management | Mostly automatic                  | Explicit publishing and removal      |
