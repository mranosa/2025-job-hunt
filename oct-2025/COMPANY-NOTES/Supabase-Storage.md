# Supabase - Software Engineer (Storage) - APAC

**Priority**: ⭐⭐⭐ Must Study
**Fit Score**: 9/10
**Location**: Remote APAC

---

## Company Overview

**About Supabase:**
- Open-source Firebase alternative
- PostgreSQL-based backend-as-a-service
- YC-backed, Series B ($80M raised)
- 100% remote, global team
- Developer-first philosophy
- Strong open-source community

**Mission**: "Make PostgreSQL as easy to use as Firebase"

**Tech Stack**: TypeScript, Node.js, PostgreSQL, AWS, Deno

**Company Size**: ~50-100 employees

**Website**: [supabase.com](https://supabase.com)
**GitHub**: [github.com/supabase](https://github.com/supabase)

---

## Position Details

**Role**: Software Engineer - Storage (APAC)

**Key Responsibilities:**
- Build and maintain Supabase Storage features
- Work on file uploads, management, and CDN integration
- PostgreSQL and AWS S3 integration
- Performance optimization for large files
- API design for storage operations

**Tech Requirements:**
- TypeScript (strong)
- Node.js backend development
- PostgreSQL experience
- AWS S3 or similar object storage
- RESTful API design
- Performance optimization

**Nice to Have:**
- Open-source contributions
- Database internals knowledge
- CDN experience
- Distributed systems

---

## Interview Process

**Stages** (4-5 rounds):

1. **Initial Screen** (30 min)
   - Recruiter or engineering manager
   - Background, experience overview
   - Culture fit, remote work discussion

2. **Technical Screen** (60 min)
   - Live coding challenge (TypeScript/Node.js)
   - Database query optimization
   - API design discussion

3. **Take-Home Assignment** (2-3 hours)
   - Real Supabase-like feature implementation
   - Storage or database-related problem
   - Code quality, testing, documentation evaluated

4. **Technical Deep Dive** (60 min)
   - Review take-home assignment
   - System design: Storage architecture at scale
   - PostgreSQL performance discussion

5. **Culture Fit / Founder Round** (30 min)
   - Async work style, remote collaboration
   - Open-source philosophy
   - Vision alignment

**Timeline**: 2-3 weeks total

---

## Technical Focus Areas

### 1. PostgreSQL Deep Dive (High Priority)

**Topics to Master:**
- **Query Optimization**:
  - EXPLAIN ANALYZE usage
  - Index strategies (B-tree, GiST, GIN, BRIN)
  - Query planning and execution

- **Performance Tuning**:
  - Connection pooling (pgBouncer)
  - Vacuum and autovacuum
  - WAL (Write-Ahead Logging)
  - Replication strategies

- **Advanced Features**:
  - Row-Level Security (RLS)
  - JSONB performance
  - Full-text search
  - PostgreSQL extensions

**Study Time**: 8-10 hours

**Resources**:
- Supabase documentation on PostgreSQL
- "PostgreSQL: Up and Running" book
- Supabase YouTube channel

---

### 2. Object Storage & CDN (High Priority)

**Topics to Master:**
- **AWS S3**:
  - Bucket policies and permissions
  - Signed URLs and presigned uploads
  - Multipart uploads
  - Lifecycle policies

- **File Management**:
  - Image transformation pipelines
  - Video encoding and streaming
  - Large file handling (chunking)

- **CDN Integration**:
  - CloudFront or similar
  - Cache invalidation
  - Edge optimization

**Study Time**: 6-8 hours

---

### 3. TypeScript & Node.js (Medium Priority)

**Topics to Master:**
- TypeScript advanced types and generics
- Node.js streams for large files
- Async/await patterns
- Error handling in async code
- Testing (Jest, supertest)

**Study Time**: 5-7 hours

---

### 4. API Design (Medium Priority)

**Topics to Master:**
- RESTful API best practices
- API versioning
- Rate limiting
- Pagination strategies
- Error response standards

**Study Time**: 4-5 hours

---

## Common Interview Questions

### Technical Questions

**PostgreSQL:**
1. "How would you optimize a slow query in PostgreSQL?"
   - Use EXPLAIN ANALYZE
   - Identify missing indexes
   - Consider query rewriting
   - Check statistics and vacuuming

2. "Explain PostgreSQL Row-Level Security and its use cases"
   - Policy-based access control at row level
   - Used in Supabase for multi-tenancy
   - Example: Users can only see their own rows

3. "How does PostgreSQL handle JSONB data? How would you index it?"
   - Binary JSON storage, faster than JSON
   - GIN indexes for JSONB columns
   - Supports path-based queries

**Storage:**
4. "Design a file upload system that handles 1TB uploads"
   - Multipart upload (chunks)
   - Resumable uploads
   - Progress tracking
   - Error handling and retries

5. "How would you implement signed URLs for secure file access?"
   - Generate time-limited URLs
   - HMAC signature with secret key
   - Include expiration timestamp
   - Validate on access

6. "Explain strategies for handling concurrent file uploads to the same location"
   - Optimistic locking with versions
   - File-level locks
   - Atomic operations
   - Conflict resolution strategies

**System Design:**
7. "Design Supabase Storage for 1 million users uploading files"
   - S3 for object storage
   - PostgreSQL for metadata
   - CDN for distribution
   - Load balancer for API servers
   - Consider: sharding, caching, replication

8. "How would you implement real-time updates for file changes?"
   - PostgreSQL triggers
   - WebSocket connections
   - Event-driven architecture
   - Consider scalability

---

### Coding Challenges (Take-Home Style)

**Challenge 1: File Upload API**
```
Implement a RESTful API for file uploads:
- POST /storage/upload (multipart form)
- GET /storage/:id (retrieve file)
- DELETE /storage/:id (delete file)
- Support for presigned URLs
- Size limits and validation
- Error handling

Tech: TypeScript, Node.js, PostgreSQL (metadata)
Time: 2-3 hours
```

**Challenge 2: Storage Bucket Manager**
```
Implement a bucket management system:
- Create/delete buckets
- Set bucket permissions
- List files in bucket
- Implement RLS policies
- Query optimization for large buckets

Tech: TypeScript, PostgreSQL, Row-Level Security
Time: 2-3 hours
```

---

## Behavioral Questions

**Supabase Culture Focus:**
- Developer-first mindset
- Open-source contribution
- Async/remote work excellence
- Shipping speed over perfection
- Direct communication

**Common Questions:**
1. "Why Supabase specifically? What appeals to you about our mission?"
   - Talk about open-source philosophy
   - PostgreSQL passion
   - Developer tools impact
   - Remote work alignment

2. "Tell me about your experience with open-source projects"
   - Contributions you've made
   - Value of community
   - Collaborative development

3. "How do you handle working asynchronously across time zones?"
   - Documentation practices
   - Async communication tools
   - Self-directed work examples

4. "Describe a time you shipped something quickly that wasn't perfect"
   - Supabase values speed
   - MVP approach
   - Iterative improvement

5. "Tell me about debugging a complex production issue"
   - Technical depth
   - Problem-solving approach
   - Communication during incidents

---

## Study Plan

**Total Prep Time**: 25-30 hours

**Week 1: Technical Foundation (15-18 hours)**
- Day 1-2: PostgreSQL deep dive (8 hours)
- Day 3-4: Object storage & AWS S3 (6 hours)
- Day 5: Review Supabase architecture (2-3 hours)

**Week 2: Practice & Polish (10-12 hours)**
- Day 1-2: Build a storage API (take-home practice)
- Day 3: System design practice (storage at scale)
- Day 4: Behavioral prep (STAR stories for async work)
- Day 5: Mock interview

---

## Resources & Links

**Official:**
- [Supabase Documentation](https://supabase.com/docs)
- [Supabase Storage Docs](https://supabase.com/docs/guides/storage)
- [Supabase GitHub](https://github.com/supabase/supabase)
- [Supabase Blog](https://supabase.com/blog)

**Technical:**
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/)
- [PostgreSQL Performance](https://www.postgresql.org/docs/current/performance-tips.html)

**Community:**
- [Supabase Discord](https://discord.supabase.com)
- [Supabase Twitter](https://twitter.com/supabase)

**Practice:**
- Build a simple storage API with PostgreSQL
- Explore Supabase codebase on GitHub
- Read Supabase engineering blog posts

---

## Key Talking Points

**"Why Supabase?"**
> "I'm passionate about developer tools and open-source software. Supabase's mission to make PostgreSQL accessible resonates with me because [personal reason]. I've used Supabase in [personal project] and was impressed by [specific feature]. I'd love to contribute to [specific area like storage] because [technical interest]."

**"Why Storage Role?"**
> "File storage and management at scale is a fascinating problem. I've worked with [AWS S3 / object storage] before and understand the challenges of [performance / security / scalability]. I'm excited about Supabase's approach to [specific storage feature]."

**Questions to Ask Interviewer:**
1. "What are the biggest technical challenges the Storage team is facing?"
2. "How does Supabase handle edge cases like very large files or high concurrent uploads?"
3. "What's the team's approach to balancing new features vs. performance optimization?"
4. "Can you tell me about the team's async communication practices?"
5. "What does success look like for this role in the first 6 months?"

---

## Red Flags to Watch For
- None major - Supabase is well-funded and growing
- Remote work requires strong self-direction
- Fast-paced environment might be intense
- Open-source means public scrutiny

## Green Flags
- ✅ Strong product-market fit
- ✅ Experienced team (ex-GitLab, Stripe, etc.)
- ✅ Active community
- ✅ Well-funded (Series B)
- ✅ 100% remote, async-first
- ✅ Developer-focused mission

---

**Last updated**: 2025-10-28
