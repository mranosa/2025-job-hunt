# System Design Cheat Sheet

Quick reference guide for system design interviews covering scalability, reliability, and architecture patterns.

---

## Table of Contents
1. [System Design Framework](#system-design-framework)
2. [Scalability Patterns](#scalability-patterns)
3. [Database Design](#database-design)
4. [Caching Strategies](#caching-strategies)
5. [Load Balancing](#load-balancing)
6. [Microservices](#microservices)
7. [Message Queues](#message-queues)
8. [Real-Time Systems](#real-time-systems)
9. [Security & Authentication](#security--authentication)
10. [Common System Designs](#common-system-designs)

---

## System Design Framework

### Step-by-Step Approach (45-60 min interview)

**1. Clarify Requirements (5-7 min)**
- Functional requirements: What features?
- Non-functional requirements: Scale, performance, consistency
- Constraints: Budget, timeline, existing systems

**2. Estimate Scale (3-5 min)**
- Users: DAU (Daily Active Users), MAU (Monthly)
- Traffic: QPS (Queries Per Second), peak load
- Storage: Data size, growth rate
- Bandwidth: Upload/download

**3. Define APIs (5 min)**
- REST endpoints or RPC methods
- Request/response formats
- Key operations

**4. High-Level Design (10-15 min)**
- Draw architecture diagram
- Identify major components
- Explain data flow

**5. Deep Dive (15-20 min)**
- Database schema
- Scaling bottlenecks
- Trade-offs and alternatives

**6. Discuss Trade-offs (5 min)**
- CAP theorem considerations
- Consistency vs availability
- Cost vs performance

---

## Scalability Patterns

### Horizontal vs Vertical Scaling

| Aspect | Horizontal (Scale Out) | Vertical (Scale Up) |
|--------|----------------------|---------------------|
| Method | Add more machines | Increase machine resources |
| Cost | Cheaper per unit | More expensive |
| Limit | Nearly unlimited | Hardware limits |
| Complexity | Higher (load balancing) | Lower (simpler) |
| Best For | Stateless services | Databases, caches |

---

### Database Sharding

**Sharding Strategies:**

1. **Range-Based Sharding**
   ```
   Shard 1: Users A-M
   Shard 2: Users N-Z
   ```
   - Pros: Easy to implement, range queries efficient
   - Cons: Uneven distribution, hotspots

2. **Hash-Based Sharding**
   ```
   Shard = hash(user_id) % num_shards
   ```
   - Pros: Even distribution
   - Cons: Rebalancing difficult, no range queries

3. **Consistent Hashing**
   ```
   Hash ring with virtual nodes
   Minimizes redistribution when nodes added/removed
   ```
   - Pros: Easy to scale, minimal data movement
   - Cons: Complex implementation

**Example:**
```
Users table sharded by user_id:
- Shard 1: user_id % 4 == 0
- Shard 2: user_id % 4 == 1
- Shard 3: user_id % 4 == 2
- Shard 4: user_id % 4 == 3
```

---

### Replication

**Master-Slave Replication:**
```
Master (writes) → Slave 1 (reads)
                → Slave 2 (reads)
                → Slave 3 (reads)
```
- Pros: Scales reads, data redundancy
- Cons: Replication lag, single write point

**Master-Master Replication:**
```
Master 1 ↔ Master 2
```
- Pros: Write scalability, high availability
- Cons: Conflict resolution needed, complexity

---

## Database Design

### CAP Theorem

**Pick 2 of 3:**
- **C**onsistency: All nodes see same data
- **A**vailability: Every request gets response
- **P**artition Tolerance: System works despite network failures

**Examples:**
- **CP**: MongoDB, HBase, Redis (strong consistency)
- **AP**: Cassandra, DynamoDB, CouchDB (eventual consistency)
- **CA**: Traditional RDBMS (assumes no partitions)

---

### SQL vs NoSQL

| Feature | SQL (PostgreSQL, MySQL) | NoSQL (MongoDB, Cassandra) |
|---------|----------------------|---------------------------|
| Schema | Fixed schema | Flexible/dynamic |
| Scaling | Vertical (harder horizontal) | Horizontal (designed for it) |
| ACID | Strong ACID | Eventual consistency |
| Joins | Supported | Limited/none |
| Use Case | Complex queries, transactions | Large-scale, flexible data |

---

### Indexing Strategies

**B-Tree Index:**
```sql
CREATE INDEX idx_email ON users(email);
```
- Default for most databases
- Good for range queries, sorting
- O(log n) lookup

**Hash Index:**
```sql
CREATE INDEX idx_id USING HASH ON users(id);
```
- O(1) lookup for exact matches
- No range queries

**Composite Index:**
```sql
CREATE INDEX idx_name_age ON users(last_name, first_name, age);
```
- Follows leftmost prefix rule
- Query can use (last_name) or (last_name, first_name) or all three

**When to Index:**
- Columns in WHERE, JOIN, ORDER BY clauses
- Foreign keys
- High cardinality columns

**When NOT to Index:**
- Small tables (full scan faster)
- Frequently updated columns
- Low cardinality columns (gender, boolean)

---

## Caching Strategies

### Cache Patterns

**1. Cache-Aside (Lazy Loading)**
```python
def get_user(user_id):
    # Check cache first
    user = cache.get(user_id)
    if user:
        return user

    # Cache miss: fetch from DB
    user = db.query("SELECT * FROM users WHERE id = ?", user_id)
    cache.set(user_id, user, ttl=3600)
    return user
```
- Pros: Only cache what's needed, resilient to cache failures
- Cons: Cache miss penalty, stale data possible

**2. Write-Through**
```python
def update_user(user_id, data):
    # Update DB first
    db.update(user_id, data)

    # Then update cache
    cache.set(user_id, data, ttl=3600)
```
- Pros: Cache always consistent, no stale data
- Cons: Write latency, unnecessary cache writes

**3. Write-Behind (Write-Back)**
```python
def update_user(user_id, data):
    # Update cache immediately
    cache.set(user_id, data)

    # Async write to DB
    queue.enqueue(lambda: db.update(user_id, data))
```
- Pros: Fast writes, reduced DB load
- Cons: Data loss risk, complexity

---

### Cache Invalidation

**Strategies:**
1. **TTL (Time To Live)**: Cache expires after fixed time
2. **Event-Driven**: Invalidate on specific events (update, delete)
3. **Versioning**: Version keys (user:123:v2)
4. **Manual**: Admin trigger for specific keys

**Thundering Herd Problem:**
```
Problem: Many requests hit DB when cache expires
Solution: Mutex/lock on cache refresh
```

```python
import threading

lock = threading.Lock()

def get_with_lock(key):
    value = cache.get(key)
    if value:
        return value

    with lock:
        # Double-check inside lock
        value = cache.get(key)
        if value:
            return value

        value = db.get(key)
        cache.set(key, value)
        return value
```

---

### CDN (Content Delivery Network)

```
User Request → CDN Edge Server (cache hit) → Return
           ↓ (cache miss)
         Origin Server → CDN caches → User
```

**What to CDN:**
- Static assets (images, CSS, JS, videos)
- Infrequently changing content (blog posts)
- Public content

**What NOT to CDN:**
- User-specific data
- Frequently changing data
- Private/authenticated content

---

## Load Balancing

### Load Balancing Algorithms

**1. Round Robin**
```
Request 1 → Server A
Request 2 → Server B
Request 3 → Server C
Request 4 → Server A  (cycle repeats)
```
- Simple, fair distribution
- Doesn't consider server load

**2. Least Connections**
```
Routes to server with fewest active connections
```
- Better for long-lived connections
- More complex to implement

**3. Weighted Round Robin**
```
Server A (weight 3): Gets 3/6 requests
Server B (weight 2): Gets 2/6 requests
Server C (weight 1): Gets 1/6 requests
```
- Handles heterogeneous servers
- Requires capacity knowledge

**4. IP Hash**
```
hash(client_ip) % num_servers
```
- Consistent client → server mapping
- Good for session affinity

---

### Layer 4 vs Layer 7 Load Balancing

| Feature | Layer 4 (Transport) | Layer 7 (Application) |
|---------|---------------------|---------------------|
| Decision Based On | IP, Port | HTTP headers, URL, cookies |
| Speed | Faster | Slower (deeper inspection) |
| Features | Simple routing | Content-based routing, SSL termination |
| Examples | AWS NLB, HAProxy TCP | AWS ALB, Nginx, HAProxy HTTP |

---

### Health Checks

```python
# Active health check
def check_health(server):
    try:
        response = requests.get(f"{server}/health", timeout=2)
        return response.status_code == 200
    except:
        return False

# Passive health check
# Monitor actual traffic, remove server after N failures
```

---

## Microservices

### Microservices vs Monolith

| Aspect | Monolith | Microservices |
|--------|----------|---------------|
| Deployment | Single unit | Independent services |
| Scaling | Scale entire app | Scale services individually |
| Technology | Single stack | Polyglot |
| Complexity | Simpler | Higher (distributed systems) |
| Development | Easier to start | Organizational scalability |

---

### Service Communication

**Synchronous (REST/gRPC):**
```
Service A → HTTP/gRPC → Service B → Response
```
- Pros: Simple, immediate response
- Cons: Tight coupling, cascading failures

**Asynchronous (Message Queue):**
```
Service A → Message Queue → Service B
```
- Pros: Loose coupling, resilient
- Cons: Eventual consistency, complexity

---

### Saga Pattern
Distributed transaction coordination.

**Choreography (Event-Driven):**
```
Order Service → OrderCreated event
Payment Service (listens) → PaymentProcessed event
Inventory Service (listens) → InventoryReserved event
```

**Orchestration (Centralized):**
```
Saga Orchestrator:
1. Call Order Service
2. Call Payment Service
3. Call Inventory Service
4. If any fails, compensate (rollback)
```

---

## Message Queues

### Kafka Architecture

```
Producers → Topic (Partitions) → Consumer Groups
```

**Key Concepts:**
- **Topic**: Category of messages
- **Partition**: Ordered sequence within topic (parallel processing)
- **Consumer Group**: Load balancing across consumers
- **Offset**: Position in partition

**Ordering Guarantees:**
- Within partition: Ordered
- Across partitions: No ordering

**Delivery Semantics:**
1. **At-most-once**: Fire and forget (fast, may lose)
2. **At-least-once**: Retry on failure (duplicates possible)
3. **Exactly-once**: Complex, slower (idempotent processing)

---

### Queue vs Pub/Sub

**Queue (Point-to-Point):**
```
Producer → Queue → Consumer (one consumer processes each message)
```
- Use: Task distribution, work queues

**Pub/Sub (Broadcast):**
```
Publisher → Topic → Subscriber 1
                  → Subscriber 2
                  → Subscriber 3
```
- Use: Event notifications, real-time updates

---

## Real-Time Systems

### WebSocket Architecture

```
Client ←→ WebSocket ←→ Server
   (persistent bi-directional connection)
```

**Scaling WebSockets:**
```
Clients → Load Balancer (sticky sessions)
       → WebSocket Server 1 → Redis Pub/Sub
       → WebSocket Server 2 → Redis Pub/Sub
       → WebSocket Server 3 → Redis Pub/Sub
```

**Key Considerations:**
- **Sticky sessions**: Route same client to same server
- **Message broker**: Distribute messages across servers
- **Heartbeats**: Detect dead connections
- **Graceful degradation**: Fallback to polling

---

### WebSocket vs HTTP Polling vs SSE

| Feature | WebSocket | HTTP Polling | Server-Sent Events |
|---------|-----------|-------------|-------------------|
| Direction | Bi-directional | Client → Server | Server → Client |
| Overhead | Low (persistent) | High (repeated requests) | Medium |
| Real-Time | Yes | No (delayed) | Yes |
| Use Case | Chat, gaming | Simple updates | Live feeds, notifications |

---

### Operational Transformation (OT) vs CRDT

**For Collaborative Editing:**

**Operational Transformation:**
```
User A: Insert "a" at position 5
User B: Insert "b" at position 5 (simultaneously)
→ Server transforms operations to converge
```
- Pros: Efficient, widely used (Google Docs)
- Cons: Complex, requires server

**CRDT (Conflict-Free Replicated Data Types):**
```
Each operation has unique ID, merge algorithm guarantees convergence
```
- Pros: No central server needed, eventual consistency guaranteed
- Cons: Higher memory, complex implementation

---

## Security & Authentication

### Authentication Methods

**1. Session-Based:**
```
User login → Server creates session → Returns session ID (cookie)
Future requests include session ID
```
- Pros: Server controls revocation
- Cons: Server state, not scalable

**2. JWT (JSON Web Token):**
```
User login → Server signs JWT → Client stores JWT
Future requests include JWT in header
```
- Pros: Stateless, scalable
- Cons: Hard to revoke, token size

**JWT Structure:**
```
header.payload.signature
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiIxMjMifQ.signature
```

**3. OAuth 2.0:**
```
User → Authorization Server → Access Token
→ Resource Server (validates token)
```
- Use: Third-party authentication (Google, GitHub)

---

### API Security

**Rate Limiting:**
```python
# Token bucket algorithm
class RateLimiter:
    def __init__(self, capacity, refill_rate):
        self.capacity = capacity
        self.tokens = capacity
        self.refill_rate = refill_rate  # tokens per second
        self.last_refill = time.time()

    def allow_request(self):
        self._refill()
        if self.tokens >= 1:
            self.tokens -= 1
            return True
        return False

    def _refill(self):
        now = time.time()
        elapsed = now - self.last_refill
        self.tokens = min(self.capacity, self.tokens + elapsed * self.refill_rate)
        self.last_refill = now
```

**API Keys:**
- Include in header: `Authorization: Bearer <key>`
- Hash and store in database
- Rotate regularly

---

## Common System Designs

### 1. URL Shortener (like Bit.ly)

**Requirements:**
- Shorten long URL to short URL
- Redirect short URL to long URL
- 100M URLs, 1000 QPS

**API:**
```
POST /api/shorten
{
  "long_url": "https://example.com/very/long/url"
}
→ Returns: "https://short.ly/abc123"

GET /abc123 → Redirect to long URL
```

**Design:**
```
Database Schema:
urls table:
- id (bigint, auto-increment)
- short_code (varchar(10), unique, indexed)
- long_url (text)
- created_at (timestamp)
- clicks (int)

short_code generation:
- Base62 encode(id)  or
- Random 7-char string + collision check
```

**Architecture:**
```
Client → Load Balancer → App Servers → Cache (Redis)
                                     ↓
                                   Database
```

**Scaling:**
- Cache popular URLs (80/20 rule)
- Database sharding by short_code
- CDN for redirects

---

### 2. Twitter Feed

**Requirements:**
- Post tweet (140 chars)
- Follow users
- View feed (tweets from followed users)
- 300M users, 100M DAU

**API:**
```
POST /api/tweet
{
  "user_id": 123,
  "content": "Hello world"
}

GET /api/feed?user_id=123
→ Returns tweets from followed users (sorted by time)
```

**Design Approaches:**

**Fan-Out on Write:**
```
User posts tweet →
  For each follower:
    Insert tweet into follower's feed cache
```
- Pros: Fast read (pre-computed)
- Cons: Slow write for celebrities (millions of followers)

**Fan-Out on Read:**
```
User requests feed →
  Fetch all followed users
  Fetch tweets from each
  Merge and sort
```
- Pros: Fast write
- Cons: Slow read (many queries)

**Hybrid Approach:**
```
- Regular users: Fan-out on write
- Celebrities (>1M followers): Fan-out on read
- Merge both at read time
```

**Schema:**
```
tweets table:
- id, user_id, content, created_at

follows table:
- follower_id, followee_id

feed_cache (Redis):
- user:{id}:feed → List of tweet IDs
```

---

### 3. Instagram (Photo Sharing)

**Requirements:**
- Upload photos
- Follow users
- View feed (photos from followed users)
- 1B users, 500M DAU
- 1M photos/day avg

**Storage Calculation:**
```
Average photo: 2MB
Daily: 1M photos × 2MB = 2TB/day
Yearly: 2TB × 365 = 730TB/year
With 3 replicas: 2.2PB/year
```

**Design:**
```
Upload Flow:
Client → App Server → Object Storage (S3)
                   → Metadata DB (photo_id, user_id, url)
                   → Queue (async processing)
                   → Image Processing (thumbnails, filters)
                   → CDN

Feed Generation:
Similar to Twitter feed (hybrid fan-out)
```

**Data Sharding:**
```
Shard by user_id for:
- User data
- Photos metadata
- Feed cache

Object storage handles photos (S3 auto-scales)
```

---

### 4. Netflix (Video Streaming)

**Requirements:**
- Upload videos
- Stream videos
- Recommend videos
- 200M users, 100M concurrent streams

**Architecture:**
```
Upload:
Client → Upload Service → Transcoding Queue
                       → Video Processing (multiple qualities)
                       → CDN (edge servers)

Streaming:
Client → CDN (closest edge) → Stream video
      ↓ (cache miss)
    Origin Server → CDN
```

**Adaptive Bitrate Streaming:**
```
Video encoded at multiple bitrates:
- 4K (25 Mbps)
- 1080p (5 Mbps)
- 720p (2.5 Mbps)
- 480p (1 Mbps)

Client measures bandwidth → Switches quality dynamically
```

**Database:**
```
videos table: id, title, description, upload_date
video_files table: video_id, quality, file_url
user_watch_history: user_id, video_id, position, timestamp
```

---

### 5. Uber (Ride Sharing)

**Requirements:**
- Riders request rides
- Match with nearby drivers
- Track ride in real-time
- 10M daily rides, 1M concurrent users

**Geo-Spatial Indexing:**
```
QuadTree or Geohash for driver locations

Geohash example:
Location (lat, lng) → Geohash string "9q8yy"
Nearby drivers: Query same prefix
```

**Architecture:**
```
Rider App ←WebSocket→ Backend ←→ Driver App
                        ↓
                 Matching Service
                        ↓
                 Location DB (spatial index)
                        ↓
                    Redis (driver locations updated every 5s)
```

**Matching Algorithm:**
```
1. Get rider location
2. Query nearby drivers (within 5km radius)
3. Filter available drivers
4. Rank by distance, rating
5. Send request to top driver
6. If declined, try next
```

**Real-Time Tracking:**
```
Driver location updates → WebSocket → Rider app
Every 5 seconds
```

---

## Key Metrics to Know

### Performance Metrics
- **Latency**: p50, p95, p99 (50th, 95th, 99th percentile)
- **Throughput**: Requests per second (RPS), Queries per second (QPS)
- **Availability**: 99.9% (three nines) = 43.8 min downtime/month

### Back-of-the-Envelope Calculations
```
1 million requests/day = ~12 requests/second
1 billion requests/month = ~400 requests/second

Storage:
1 char = 1 byte
1 KB = 1,000 bytes
1 MB = 1,000 KB
1 GB = 1,000 MB
1 TB = 1,000 GB
1 PB = 1,000 TB
```

---

## Interview Tips

1. **Ask Clarifying Questions**: Don't assume, ask about scale, requirements
2. **Start Simple**: Begin with single-server design, then scale
3. **Think Out Loud**: Explain your reasoning
4. **Draw Diagrams**: Visual representation helps
5. **Discuss Trade-offs**: No perfect solution, explain pros/cons
6. **Numbers Matter**: Estimate scale, storage, bandwidth
7. **Know Your Tools**: When to use Redis vs Memcached, SQL vs NoSQL
8. **Failure Scenarios**: Consider what happens when components fail
9. **Security**: Don't forget authentication, encryption
10. **Monitoring**: How would you detect issues?

---

*Last updated: 2025-10-28*
