# 5-Day Interview Preparation Study Plan

**Total Time Investment:** 22.5 hours (5 days × 3 sessions × 1.5 hours)
**Target:** 23 positions across Remote Global/APAC, Japan, and Finland
**Format:** Each session = 1 hour learning (video + practice) + 30 minutes quiz

---

## Study Schedule Overview

| Day | Focus Area | Sessions |
|-----|-----------|----------|
| Day 1 | Algorithms & Data Structures | Arrays/Strings, Trees/Graphs, Dynamic Programming |
| Day 2 | TypeScript & React | Advanced TS, React Patterns, Testing |
| Day 3 | System Design | Scalability/DBs, Caching, Microservices |
| Day 4 | Backend & Specialized | Go/Node.js, Blockchain, Real-Time |
| Day 5 | Behavioral & Company Prep | STAR Method, Company Research, Mock Interview |

---

## Day 1: Algorithms & Data Structures Foundation

### Session 1 (Morning): Arrays, Strings, Hash Maps

**Main Video Resource:**
- [NeetCode - "Sliding Window Technique Explained"](https://www.youtube.com/watch?v=jM2dhDPYMQM) (30 min)

**Learning (1 hour):**
1. Watch the NeetCode video on sliding window technique
2. Study these patterns:
   - **Two Pointers**: Left and right pointer approach for sorted arrays
   - **Sliding Window**: Fixed or variable window for substring/subarray problems
   - **Hash Maps**: O(1) lookup for frequency counting and pair finding

**Key Concepts:**
- Time complexity: O(n) vs O(n²)
- Space-time tradeoffs with hash maps
- When to use two pointers vs sliding window

**Quiz (30 minutes):**
1. LeetCode #1 - Two Sum (Easy)
2. LeetCode #3 - Longest Substring Without Repeating Characters (Medium)
3. LeetCode #242 - Valid Anagram (Easy)
4. LeetCode #125 - Valid Palindrome (Easy)

**Success Criteria:** Solve 3/4 problems without hints

---

### Session 2 (Afternoon): Trees & Graphs Basics

**Main Video Resource:**
- [Back To Back SWE - "Tree Traversals - Inorder, Preorder, Postorder"](https://www.youtube.com/watch?v=gm8DUJJhmY4) (45 min)

**Learning (1 hour):**
1. Watch the tree traversal video
2. Study these patterns:
   - **Binary Tree Traversals**: Inorder, preorder, postorder (recursive and iterative)
   - **BFS (Breadth-First Search)**: Level-order traversal with queue
   - **DFS (Depth-First Search)**: Exploring paths with stack/recursion

**Key Concepts:**
- Recursive vs iterative approaches
- Queue for BFS, Stack for DFS
- Tree vs graph (cycles, visited tracking)

**Quiz (30 minutes):**
1. LeetCode #104 - Maximum Depth of Binary Tree (Easy)
2. LeetCode #100 - Same Tree (Easy)
3. LeetCode #226 - Invert Binary Tree (Easy)
4. LeetCode #102 - Binary Tree Level Order Traversal (Medium)

**Success Criteria:** Implement both recursive and iterative solutions for at least 1 problem

---

### Session 3 (Evening): Dynamic Programming Introduction

**Main Video Resource:**
- [Errichto - "Dynamic Programming Introduction"](https://www.youtube.com/watch?v=YBSt1jYwVfU) (50 min)

**Learning (1 hour):**
1. Watch Errichto's DP introduction
2. Study these patterns:
   - **Memoization**: Top-down approach with caching
   - **Tabulation**: Bottom-up approach with array
   - **State Definition**: Identifying subproblems

**Key Concepts:**
- Overlapping subproblems
- Optimal substructure
- When to use DP vs greedy vs divide-and-conquer

**Quiz (30 minutes):**
1. LeetCode #70 - Climbing Stairs (Easy)
2. LeetCode #198 - House Robber (Medium)
3. LeetCode #322 - Coin Change (Medium)

**Success Criteria:** Explain both memoization and tabulation approaches for 1 problem

---

## Day 2: TypeScript & React Fundamentals

### Session 1 (Morning): TypeScript Advanced Features

**Main Video Resources:**
- [Matt Pocock - "TypeScript Generics are Easy"](https://www.youtube.com/watch?v=EcCTIExsqmI) (25 min)
- [Matt Pocock - "TypeScript Utility Types"](https://www.youtube.com/watch?v=EU0TB_8KHpY) (15 min)

**Learning (1 hour):**
1. Watch both Matt Pocock videos
2. Study these concepts:
   - **Generics**: Type parameters, constraints, default types
   - **Utility Types**: Partial, Pick, Omit, Record, Exclude, Extract
   - **Type Guards**: typeof, instanceof, custom type predicates
   - **Advanced Types**: Union, intersection, conditional types

**Key Concepts:**
- Type inference and type narrowing
- Generic constraints with extends
- Creating reusable type-safe utilities

**Quiz (30 minutes):**
1. Create a type-safe API wrapper with generics
2. Implement custom utility types: DeepPartial, DeepReadonly
3. Build type guards for runtime type checking
4. Create a typed EventEmitter class

**Success Criteria:** All code compiles with strict TypeScript settings

---

### Session 2 (Afternoon): React Core Patterns

**Main Video Resource:**
- [Jack Herrington - "Five Clever Hacks for React Hooks"](https://www.youtube.com/watch?v=feTv8ZGVdNg) (35 min)

**Learning (1 hour):**
1. Watch Jack Herrington's hooks video
2. Study these patterns:
   - **Performance Optimization**: useMemo, useCallback, React.memo
   - **Custom Hooks**: Extracting logic, composition patterns
   - **Side Effects**: useEffect cleanup, dependency arrays
   - **State Management**: useState vs useReducer

**Key Concepts:**
- When to optimize (measure first!)
- Stale closures and dependency arrays
- Custom hook design patterns
- Component composition over inheritance

**Quiz (30 minutes):**
1. Build a custom `useFetch` hook with loading/error states
2. Optimize a component with excessive re-renders
3. Create a `useDebounce` hook
4. Implement `useLocalStorage` with sync across tabs

**Success Criteria:** Hooks work correctly and demonstrate understanding of dependencies

---

### Session 3 (Evening): State Management & Testing

**Main Video Resource:**
- [Web Dev Simplified - "React Testing Library Crash Course"](https://www.youtube.com/watch?v=JKOwJUM4_RM) (45 min)

**Learning (1 hour):**
1. Watch Web Dev Simplified's testing video
2. Study these concepts:
   - **Context API**: Provider pattern, avoiding prop drilling
   - **React Testing Library**: Testing user behavior, not implementation
   - **Testing Patterns**: Arrange-Act-Assert, mocking, async testing

**Key Concepts:**
- Context performance considerations
- Query priorities: getByRole > getByLabelText > getByTestId
- Testing async operations (waitFor, findBy)
- User-centric testing approach

**Quiz (30 minutes):**
1. Create a form component with validation
2. Write tests for the form (validation, submission, error handling)
3. Test async data fetching component
4. Test component with Context

**Success Criteria:** All tests pass and cover happy path + error cases

---

## Day 3: System Design Fundamentals

### Session 1 (Morning): Scalability & Database Design

**Main Video Resources:**
- [ByteByteGo - "CAP Theorem Explained"](https://www.youtube.com/watch?v=k-Yaq8AHlFA) (15 min)
- [ByteByteGo - "Database Sharding Explained"](https://www.youtube.com/watch?v=hdxdhCpgYo8) (10 min)

**Learning (1 hour):**
1. Watch both ByteByteGo videos
2. Study these concepts:
   - **CAP Theorem**: Consistency, Availability, Partition tolerance trade-offs
   - **Sharding**: Range-based, hash-based, directory-based
   - **Replication**: Master-slave, master-master, quorum
   - **Indexing**: B-tree, hash indexes, composite indexes

**Key Concepts:**
- Horizontal vs vertical scaling
- Database normalization vs denormalization
- Read replicas for scaling reads
- Consistent hashing for shard distribution

**Quiz (30 minutes):**
Design a database architecture for:
- 10 million users
- 100 million posts
- Support for: create post, get user feed, search posts
- Requirements: high availability, eventual consistency acceptable

Include: sharding strategy, replication, indexing plan

**Success Criteria:** Clear diagram with justified trade-offs

---

### Session 2 (Afternoon): Caching & Load Balancing

**Main Video Resource:**
- [Hussein Nasser - "Redis Crash Course"](https://www.youtube.com/watch?v=jgpVdJB2sKQ) (50 min)

**Learning (1 hour):**
1. Watch Hussein Nasser's Redis video
2. Study these concepts:
   - **Caching Patterns**: Cache-aside, write-through, write-behind
   - **Cache Invalidation**: TTL, event-driven, versioning
   - **Redis Data Structures**: Strings, hashes, lists, sets, sorted sets
   - **Load Balancing**: Round-robin, least connections, weighted

**Key Concepts:**
- Cache hit ratio optimization
- Thundering herd problem
- CDN for static assets
- Session persistence vs stateless design

**Quiz (30 minutes):**
Design a caching layer for e-commerce:
- Product catalog (100k products, rarely change)
- User sessions (millions of users)
- Shopping cart (real-time updates)
- Product inventory (high consistency needed)

Include: cache strategy for each, invalidation approach, CDN usage

**Success Criteria:** Different strategies for different data types, justified

---

### Session 3 (Evening): Microservices & Messaging

**Main Video Resources:**
- [ByteByteGo - "What is Kafka and How does it work?"](https://www.youtube.com/watch?v=LN_HcJVbySw) (12 min)
- [ByteByteGo - "Microservices Explained"](https://www.youtube.com/watch?v=CdBtNQZH8a4) (8 min)

**Learning (1 hour):**
1. Watch both ByteByteGo videos
2. Study these concepts:
   - **Service Decomposition**: Bounded contexts, domain-driven design
   - **Kafka Architecture**: Topics, partitions, consumer groups, offset management
   - **Event-Driven**: Event sourcing, CQRS, saga pattern
   - **Service Communication**: Sync (REST, gRPC) vs async (message queues)

**Key Concepts:**
- Microservices vs monolith trade-offs
- Data consistency across services (saga pattern)
- Message ordering and delivery guarantees
- Service discovery and API gateway

**Quiz (30 minutes):**
Design an order processing system for food delivery (like Wolt):
- Services: Order, Payment, Restaurant, Delivery, Notification
- Requirements:
  - Handle failed payments (rollback)
  - Real-time order status updates
  - Restaurant order queue
  - Driver assignment

Include: service boundaries, communication patterns, data consistency approach

**Success Criteria:** Clear service diagram with event flows and failure handling

---

## Day 4: Backend & Specialized Topics

### Session 1 (Morning): Go/Node.js Backend Patterns

**Main Video Resource:**
- [TechWorld with Nana - "Golang Tutorial for Beginners"](https://www.youtube.com/watch?v=yyUHQIec83I) (watch first 1 hour of 3.5hr video)

**Learning (1 hour):**
1. Watch first hour of Golang tutorial
2. Study these concepts:
   - **Goroutines & Channels**: Concurrent programming, channel patterns
   - **Error Handling**: Explicit errors, error wrapping
   - **Interfaces**: Implicit implementation, composition
   - **Node.js Async**: async/await, promises, event loop

**Key Concepts:**
- Go's concurrency model vs Node.js event loop
- Structured error handling
- API design patterns (REST best practices)
- Middleware and request processing

**Quiz (30 minutes):**
Implement in Go or Node.js:
1. Concurrent API client that fetches from 5 endpoints simultaneously
2. Rate limiter using goroutines/promises
3. REST API endpoint with proper error handling
4. Middleware for authentication

**Success Criteria:** Code handles errors properly and uses concurrency effectively

---

### Session 2 (Afternoon): Blockchain/DeFi Basics

**Main Video Resources:**
- [Whiteboard Crypto - "Smart Contracts Explained"](https://www.youtube.com/watch?v=ZE2HxTmxfrI) (15 min)
- [Whiteboard Crypto - "DeFi Explained"](https://www.youtube.com/watch?v=17QRFlml4pA) (20 min)

**Learning (1 hour):**
1. Watch both Whiteboard Crypto videos
2. Study these concepts:
   - **Smart Contracts**: Solidity basics, gas, deployment
   - **DeFi Protocols**: AMMs (xy=k formula), lending, staking
   - **ERC Standards**: ERC-20 tokens, ERC-721 NFTs
   - **Web3 Integration**: Ethers.js, wallet connection

**Key Concepts:**
- Immutability and security implications
- Gas optimization techniques
- Liquidity pools and LP tokens
- Oracle problem (relevant for Chainlink)

**Quiz (30 minutes):**
1. Write a simple ERC-20 token contract in Solidity
2. Explain how Uniswap AMM works (xy=k)
3. Design a staking contract architecture
4. Explain oracle design for price feeds (Chainlink-specific)

**Success Criteria:** Can explain smart contract execution and DeFi mechanics clearly

---

### Session 3 (Evening): Real-Time Systems & WebSockets

**Main Video Resource:**
- [Hussein Nasser - "WebSockets Crash Course"](https://www.youtube.com/watch?v=2Nt-ZrNP22A) (40 min)

**Learning (1 hour):**
1. Watch Hussein Nasser's WebSocket video
2. Study these concepts:
   - **WebSocket Protocol**: Handshake, frames, connection management
   - **Pub/Sub Patterns**: Redis pub/sub, message brokers
   - **Real-Time Sync**: Operational Transformation, CRDTs
   - **Connection Scaling**: Load balancing WebSockets, sticky sessions

**Key Concepts:**
- WebSocket vs HTTP polling vs Server-Sent Events
- Message ordering and delivery guarantees
- Handling disconnections and reconnections
- Presence detection and typing indicators

**Quiz (30 minutes):**
Design a real-time chat application:
- Features: 1-on-1 chat, group chat, typing indicators, read receipts
- Scale: 1 million concurrent users
- Requirements: message ordering, offline support, search history

Include: WebSocket architecture, message persistence, scaling approach

**Success Criteria:** Architecture handles scale and real-time requirements

---

## Day 5: Behavioral & Company Prep

### Session 1 (Morning): Behavioral Interview Preparation

**Main Video Resources:**
- [Exponent - "How to Answer Any Behavioral Interview Question"](https://www.youtube.com/watch?v=qVpi5s-b7dw) (25 min)
- [Exponent - "STAR Method Explained"](https://www.youtube.com/watch?v=hU6BXqJiDE8) (15 min)

**Learning (1 hour):**
1. Watch both Exponent videos
2. Prepare 7 STAR stories covering:
   - **Technical Challenge**: Complex problem you solved
   - **Failure/Mistake**: What you learned from failure
   - **Leadership**: Leading project or mentoring
   - **Conflict**: Disagreement with teammate/manager
   - **Collaboration**: Cross-functional teamwork
   - **Innovation**: Creative solution or improvement
   - **Learning**: Quickly learning new technology

**STAR Format:**
- **S**ituation: Context (1-2 sentences)
- **T**ask: Your responsibility (1 sentence)
- **A**ction: What YOU did (3-4 sentences)
- **R**esult: Outcome with metrics (1-2 sentences)

**Quiz (30 minutes):**
Practice answering out loud:
1. "Tell me about a time you faced a difficult technical challenge"
2. "Describe a situation where you had to learn something quickly"
3. "Tell me about a conflict with a teammate and how you resolved it"
4. "Give an example of when you failed and what you learned"
5. "Tell me about a time you improved a process or system"

**Success Criteria:** All 7 stories prepared, can deliver smoothly in under 2 minutes each

---

### Session 2 (Afternoon): Company Research & Culture Fit

**Main Video Resource:**
- [Clément Mihailescu - "How to Research a Company Before Your Interview"](https://www.youtube.com/watch?v=ZILebJWUp8M) (20 min)

**Learning (1 hour):**
1. Watch Clément's research guide
2. Deep dive into your **top 5 target companies**:
   - Read latest engineering blog posts
   - Study product features and user experience
   - Read Glassdoor reviews (focus on engineering culture)
   - Check recent news and funding
   - Understand company stage (startup vs established)

**For each company, prepare:**
- "Why this company?" (2-3 specific reasons)
- "Why you?" (match your skills to their needs)
- 2-3 thoughtful questions to ask interviewers

**Recommended Top 5 Target Companies** (based on fit):
1. Supabase (if strong in PostgreSQL/storage)
2. Wolt (if interested in scale/logistics)
3. Buffer (if remote work focused)
4. Chainlink Labs (if blockchain interested)
5. Beautiful.ai (if design-minded)

**Quiz (30 minutes):**
Write out answers to:
1. "Why [Company]?" for each of your top 5
2. "Why are you interested in this role?"
3. "What's a challenge [Company] might face and how would you approach it?"
4. Prepare 3 smart questions for each company

**Success Criteria:** Specific, authentic answers that show genuine research

---

### Session 3 (Evening): Mock Interview & Final Review

**Main Video Resource:**
- [NeetCode - "Mock Google Interview"](https://www.youtube.com/watch?v=kFeXwkgnQ9U) (45 min)

**Learning (1 hour):**
1. Watch NeetCode's mock interview (observe the process)
2. Conduct a **full mock interview** for yourself:
   - **Algorithm Problem** (25 min): Pick a medium LeetCode you haven't solved
     - Think out loud
     - Explain approach before coding
     - Test with examples
     - Analyze time/space complexity
   - **System Design** (25 min): Design Twitter feed or URL shortener
     - Clarify requirements
     - Draw architecture
     - Discuss trade-offs
     - Handle scale

**Quiz (30 minutes):**
1. Review weak areas from Days 1-4:
   - Revisit 2-3 algorithm problems you struggled with
   - Redraw 1 system design diagram from memory
   - Practice 1 behavioral answer

2. Create final **interview cheat sheet**:
   - Algorithm patterns quick reference
   - System design checklist
   - Your 7 STAR stories (bullet points)
   - Company-specific talking points

**Success Criteria:** Can complete mock interview smoothly, cheat sheet ready

---

## Success Metrics

### Day 1-2: Technical Fundamentals
- ✅ Solve 70%+ of coding problems independently
- ✅ Can explain time/space complexity for all solutions
- ✅ TypeScript code compiles with strict mode
- ✅ React components demonstrate best practices

### Day 3-4: System Design & Backend
- ✅ Can draw clear system architecture diagrams
- ✅ Justify trade-offs between different approaches
- ✅ Explain scaling strategies for 10M+ users
- ✅ Understand blockchain basics for Web3 roles

### Day 5: Behavioral & Company
- ✅ 7 STAR stories fully prepared
- ✅ Can answer "Why this company?" for top 5 targets
- ✅ Complete mock interview without major issues
- ✅ Final cheat sheet created

---

## Additional Resources

### Practice Platforms
- **LeetCode**: 150+ problems (NeetCode 150 list)
- **System Design**: ByteByteGo, Exponent
- **TypeScript**: TypeScript Playground, TS Challenges
- **React**: React.dev, Testing Library docs

### Reference Materials
- See `ALGORITHMS-CHEATSHEET.md` for algorithm patterns
- See `SYSTEM-DESIGN-CHEATSHEET.md` for architecture patterns
- See `BEHAVIORAL-STORIES.md` for STAR template
- See `COMPANY-NOTES/` for company-specific preparation

### After This 5-Day Plan

**Week 2-3: Deep Dive**
- Focus on 3-5 specific companies you're applying to
- Complete take-home-style projects
- Practice more system design scenarios
- Mock interviews with peers or online platforms

**Week 4+: Application & Interview Phase**
- Start applying to positions
- Continue practicing 1-2 hours daily
- Refine STAR stories based on interviews
- Update cheat sheet with learnings

---

## Tips for Success

1. **Consistency Over Intensity**: Complete all 15 sessions, even if you need to adjust timing
2. **Active Learning**: Code along with videos, don't just watch
3. **Quiz Honestly**: Don't look at solutions too quickly, struggle first
4. **Review Daily**: Spend 10 min each morning reviewing previous day
5. **Sleep Well**: 8 hours sleep crucial for memory consolidation
6. **Take Breaks**: Use Pomodoro (25 min work, 5 min break)
7. **Stay Hydrated**: Keep water nearby during sessions
8. **Minimize Distractions**: Phone in another room, close unnecessary tabs

---

## Emergency Adjustments

**If running behind schedule:**
- Skip the "nice-to-have" portions of videos
- Focus on quiz problems over video content
- Reduce from 3 to 2 sessions per day (extend to 7-8 days)

**If a topic is too easy:**
- Skip quiz and move to more challenging problems
- Use extra time for system design practice
- Dive deeper into company-specific preparation

**If a topic is too hard:**
- Extend learning time, reduce quiz time
- Watch additional videos on the topic
- Revisit fundamentals before continuing

---

**Good luck with your interview preparation! 🚀**

*Last updated: 2025-10-28*
