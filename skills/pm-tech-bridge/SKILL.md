---
name: pm-tech-bridge
description: Translate between Product Management and Engineering mindsets to reduce friction and improve collaboration. Use this skill when: (1) PMs and engineers are miscommunicating, (2) technical feasibility needs to be explained to PMs, (3) business requirements need technical translation for engineers, (4) facilitating requirements reviews or architecture discussions, (5) making trade-offs between user experience and technical constraints. This skill reveals implicit information and helps both sides reach consensus.
version: 1.0.0
source: claude-code-pm-plugin
analyzed_commits: 7
---

# PM ↔ Tech Bridge

Translate between PM and Engineering. Reduce friction. Reveal what's unsaid.

## The Core Problem

PMs and engineers speak different languages. They have different mental models, priorities, and concerns. This causes:
- Misunderstandings about requirements
- Unrealistic expectations
- Missed technical constraints
- Frustration and delays

**This skill bridges that gap.**

## Two Mindsets

### PM Mindset

**Focus**: User value, business goals, experience

**Language**: User scenarios, business flows, feature requests

**Style**: Descriptive, story-based, outcome-oriented

**Example PM statements**:
- "Users need real-time notifications"
- "Make the search faster"
- "Add AI recommendations"

**What they care about**:
- Will users like this?
- Will this move our metrics?
- Is this competitive?

**What they don't say** (but should):
- How fast is "real-time"?
- How much faster?
- What data does AI need?

### Engineering Mindset

**Focus**: Technical feasibility, system design, implementation cost

**Language**: Data structures, APIs, algorithms, infrastructure

**Style**: Precise, logical, implementation-oriented

**Example engineering statements**:
- "We need to use Redis for caching"
- "This requires a distributed transaction"
- "The API should be RESTful"

**What they care about**:
- Can we build this?
- Will it scale?
- What are the technical risks?

**What they don't say** (but should):
- Why do we need Redis?
- What problem does a distributed transaction solve for users?
- What's the user impact of this technical decision?

## Translation Patterns

### Pattern 1: PM → Tech (Business → Implementation)

When PMs describe features, translate to technical requirements.

**Example 1: "Real-time"**

**PM says**: "Users need real-time notifications"

**Engineers hear**:
```
Technical Requirement: User notification system

Questions to ask PM:
1. What does "real-time" mean?
   - <1 second? <100ms? <10ms?
2. What's the volume?
   - How many notifications/second?
3. What's the tolerance for delay?
   - Is 5 seconds acceptable?
4. What happens on failure?
   - Retry? Queue? Discard?

Technical options:
• Polling (Simple but slow: 5-30s latency)
• Server-Sent Events (SSE) (One-way, <1s latency)
• WebSockets (Bidirectional, <100ms latency)
• Push notifications (Best for mobile, variable latency)

Recommendation: Start with SSE. Upgrade to WebSockets if:
- Bidirectional communication needed
- <100ms latency is critical
- Scale justifies complexity
```

**Example 2: "Performance"**

**PM says**: "Optimize page load performance"

**Engineers hear**:
```
Technical Requirement: Page load optimization

Questions to ask PM:
1. Current state: What's the current load time?
2. Target state: What should it be? (Provide specific numbers)
3. Metric: Which metric matters?
   - First Contentful Paint (FCP)?
   - Largest Contentful Paint (LCP)?
   - Time to Interactive (TTI)?
   - Perceived load time?
4. Priority: What are we optimizing for?
   - Fast networks (3G/4G)?
   - Slow networks (2G/rural)?
   - High-end devices?
   - Low-end devices?

Technical strategies (with PM-facing trade-offs):
• Code splitting → Faster initial load, slower navigation
• Image optimization → Faster loads, quality loss possible
• Caching → Much faster repeat visits, complexity
• CDN → Faster global access, monthly cost
• Server-side rendering → Faster FCP, slower TTI, higher server cost

Need PM decision: What's acceptable?
```

**Example 3: "AI/ML"**

**PM says**: "We need smart recommendations"

**Engineers hear**:
```
Technical Requirement: Recommendation system

Questions to ask PM:
1. What are we recommending?
   - Products? Content? Users?
2. What data do we have?
   - User behavior? Item attributes? Both?
3. What's "smart"?
   - Popular items? (Baseline)
   - Collaborative filtering? (Needs user data)
   - Content-based? (Needs item metadata)
   - Deep learning? (Needs lots of data + compute)
4. How important is accuracy vs. speed?
   - Can we show okay recommendations instantly?
   - Or perfect recommendations but slowly?

Technical options with trade-offs:
• Popular items (No ML, instant, low accuracy)
• Collaborative filtering (Medium ML, fast, needs data)
• Content-based (Medium ML, fast, needs metadata)
• Hybrid/Deep learning (Complex, slower, high accuracy)

Recommendation: Start with popular items. Measure usage.
If usage justifies, upgrade to collaborative filtering.
```

### Pattern 2: Tech → PM (Implementation → Business Impact)

When engineers discuss technical options, translate to business impact.

**Example 1: "Consistency"**

**Engineer says**: "Strong consistency is too expensive. Let's use eventual consistency."

**PM hears**:
```
Technical Proposal: Use eventual consistency instead of strong consistency

Business impact:
• What changes for users:
  - When you create an order, it might not appear in your order list for 1-5 seconds
  - When you update profile, changes might not be visible immediately
  - Very rarely (<<1%), you might see stale data

• User experience impact:
  - Most users won't notice
  - Power users might see slight delays
  - Not critical for most operations

• Benefits (why do this):
  - System can handle 10x more users
  - Faster response times (200ms vs 800ms)
  - Lower infrastructure costs ($5000/month vs $20000/month)

• Risks:
  - Rare data inconsistency (temporary)
  - User confusion (unlikely but possible)

Need PM decision: Is this trade-off acceptable?
  Option A: Strong consistency (Perfect but expensive: $20k/month)
  Option B: Eventual consistency (Slight delay but scalable: $5k/month)

Recommendation: Option B, unless we have regulatory requirements
```

**Example 2: "Async Processing"**

**Engineer says**: "We should process this asynchronously with a queue."

**PM hears**:
```
Technical Proposal: Use asynchronous processing with message queue

Business impact:
• What changes for users:
  - Submit action → Get confirmation immediately
  - Actual processing happens in background (0-30 seconds)
  - User might need to wait or refresh for results

• User experience impact:
  - Feels faster (instant confirmation)
  - Might confuse users (where's my result?)
  - Need clear UI communication ("Processing...")

• Benefits:
  - System can handle spikes (Black Friday, etc.)
  - Better reliability (messages not lost)
  - Can retry failures automatically

• Cost:
  - Increased complexity
  - Delayed results
  - Infrastructure cost (queue service)

Examples users know:
- Email sending (you click send, it sends later)
- Video upload (you upload, it processes later)
- Payment processing (you pay, it confirms later)

Need PM decision: Is delayed processing acceptable?
```

**Example 3: "MVP vs Scale"**

**Engineer says**: "For MVP, let's use a simple database. We'll scale later."

**PM hears**:
```
Technical Proposal: Start simple, scale when needed

Business impact:
• Phase 1 (MVP - 0 to 10k users):
  - Simple database (PostgreSQL)
  - Fast to build (2 weeks)
  - Handles current load easily
  - Cost: $50/month

• Phase 2 (Growth - 10k to 100k users):
  - Add caching (Redis)
  - Add read replicas
  - Takes 1 week to implement
  - Cost: $500/month

• Phase 3 (Scale - 100k+ users):
  - Might need sharding or partitioning
  - Takes 4-8 weeks to implement
  - Cost: $5000+/month

• Decision timeline:
  - We'll know when to scale based on metrics
  - Can't predict exactly (depends on growth)
  - Have 1-2 months of runway before we MUST scale

• Risk:
  - If we grow VERY fast (viral), we might scramble to scale
  - Mitigation: Monitor metrics weekly, plan for scale early

Need PM decision: Is this phased approach okay?
  Or should we invest in scale from day 1? (Takes longer, costs more)
```

## Translation Tables

### PM → Tech Translation

| PM Says | Tech Understands | Technical Solution |
|---------|------------------|-------------------|
| "Real-time updates" | WebSocket/SSE/Polling | Push notification system |
| "Massive data" | Big data processing | Elasticsearch, Hadoop, etc. |
| "Smart/AI" | Machine learning algorithms | Collaborative filtering, neural nets |
| "Fast search" | Full-text search | Elasticsearch, Lucene |
| "Scalable" | Horizontal scaling | Microservices, load balancers |
| "Reliable" | Fault tolerance | Redundancy, failover, retries |
| "Secure" | Authentication/authorization | OAuth, RBAC, encryption |

### Tech → PM Translation

| Tech Says | PM Understands | Business Impact |
|-----------|----------------|-----------------|
| "Eventual consistency" | Data might be delayed slightly | Brief delay in updates |
| "Async processing" | Not instant, happens in background | User waits or sees loading state |
| "Caching" | Stores copies to be faster | Better performance, might be stale |
| "Rate limiting" | Restricts how often users can act | Prevents abuse, might block power users |
| "Degraded mode" | Some features temporarily disabled | System stays up but with reduced functionality |
| "Technical debt" | Code that needs refactoring | Faster development now, slower later |

## Common Misunderstandings

### PM Misconceptions

**"This is simple, just add a field"**
- **Reality**: Might require database migration, API changes, UI updates, data backfill
- **Translation**: "This requires schema change, API versioning, and data migration. Estimate: 2-3 days."

**"Can't we just use AI?"**
- **Reality**: AI needs data, training, infrastructure, maintenance
- **Translation**: "AI requires: training data, model training, API infrastructure. Is the problem worth this complexity?"

**"X product has it, why can't we?"**
- **Reality**: Different contexts, tech stacks, resources
- **Translation**: "X product might have 50 engineers working on this. We have 2. What's the minimum viable version?"

### Engineering Misconceptions

**"This is technically impossible"**
- **Reality**: Might be misunderstanding requirements
- **Translation**: "What specific outcome do you need? There might be simpler ways to achieve it."

**"We need to refactor everything first"**
- **Reality**: Over-engineering, low ROI
- **Translation**: "Refactoring would take 6 weeks. Is the current code blocking this feature? If yes, what's the minimal refactor needed?"

**"This feature isn't important"**
- **Reality**: Not understanding business context
- **Translation**: "Why does the business need this? What's the revenue/user impact?"

## Facilitation Techniques

### In Requirements Review

When PMs present requirements:

1. **Restate in technical terms**: "Let me translate this to technical requirements..."
2. **Ask clarification questions**: Use the question templates above
3. **Propose options with trade-offs**: Give PMs choices
4. **Validate understanding**: "Am I understanding this correctly?"

### In Technical Review

When engineers present designs:

1. **Translate to business impact**: "This technical choice means..."
2. **Explain user impact**: "Users will experience..."
3. **Highlight trade-offs**: "We're trading X for Y..."
4. **Ask for PM decision**: "Is this acceptable?"

### When They Disagree

**Step 1: Clarify the disagreement**
- Is it about feasibility? (Can we build it?)
- Is it about priorities? (Should we build it?)
- Is it about trade-offs? (What are we giving up?)

**Step 2: Gather data**
- What evidence supports each side?
- What are the assumptions?
- What's the cost of each option?

**Step 3: Propose options**
- Option A: Perfect but expensive (time/cost)
- Option B: Good enough, affordable
- Option C: MVP to test

**Step 4: Facilitate decision**
- Make trade-offs explicit
- Get data where needed
- Make a decision and move on

## When to Use This Skill

Trigger this skill when:
1. PMs and engineers are talking past each other
2. Technical feasibility needs to be explained to business stakeholders
3. Business requirements need technical clarification
4. Facilitating requirement reviews or architecture discussions
5. Making trade-offs between UX and technical constraints
6. Translating between technical and non-technical stakeholders

## Output Language

Generate translation output in Chinese for Chinese-speaking teams.

## Exit Criteria

Translation is complete when:
- Both sides understand each other's concerns
- Technical implications are clear to PMs
- Business impact is clear to engineers
- Trade-offs are explicit
- Decisions can be made with full context
