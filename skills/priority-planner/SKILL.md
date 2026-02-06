---
name: priority-roadmap-planner
description: Plan product roadmaps and prioritize features using RICE scoring and MoSCoW methods. Use this skill when: (1) resources are limited and trade-offs must be made, (2) multiple features compete for development time, (3) determining MVP scope, (4) creating phased delivery plans, (5) deciding what NOT to build. This skill helps make hard prioritization decisions with explicit trade-offs and clear rationale.
version: 1.0.0
source: claude-code-pm-plugin
analyzed_commits: 7
---

# Priority & Roadmap Planner

Make hard trade-offs with clear rationale. Decide what NOT to build.

## Core Principles

**Resources are always finite**: You can't build everything. Prioritization is mandatory.

**Value × Cost = Priority**: High value is meaningless if cost is astronomical.

**Explicit trade-offs**: Every "yes" is a "no" to something else. State it clearly.

**Courage to say no**: Not building is a valid strategy. Document why.

## Evaluation Dimensions

For each requirement/feature, assess across 5 dimensions:

### 1. User Value

**Questions**:
- How painful is the current problem? (Scale: 1-10)
- How many users affected? (Count or percentage)
- How often will this be used? (Daily/Weekly/Monthly/Rarely)
- Can users achieve this another way? (Alternatives)

**Scoring**:
- **High (10 points)**: Core pain point, affects most users, daily use, no alternatives
- **Medium (5 points)**: Important problem, some users, weekly use, poor alternatives
- **Low (1 point)**: Nice to have, few users, rare use, adequate alternatives

### 2. Business Value

**Questions**:
- What core metrics does this impact? (Revenue/Retention/Acquisition/Engagement)
- What's the quantified impact? (e.g., +20% conversion, -15% churn)
- Is this strategically important? (Alignment with company goals)
- Does this create competitive advantage?

**Scoring**:
- **High (10 points)**: Direct revenue impact, strategic must-have, competitive differentiator
- **Medium (5 points)**: Indirect value, supportive of strategy, nice-to-have
- **Low (1 point)**: Minimal business impact, misaligned with strategy

### 3. Implementation Cost

**Questions**:
- Development effort? (Person-weeks or person-months)
- Technical complexity? (Low/Medium/High)
- Resource requirements? (Backend/Frontend/DevOps/Design)
- Time to market? (Weeks/Months)

**Scoring** (Effort for RICE):
- **Low**: <1 person-week
- **Medium**: 1-4 person-weeks
- **High**: 1-3 person-months
- **Very High**: >3 person-months

### 4. Risk Assessment

**Types of risk**:
- **Technical**: Can we build it? New tech? Uncertainty?
- **Business**: Will users use it? Market fit?
- **Resource**: Do we have the skills/people?
- **Timing**: Must it be done now or can it wait?

**Scoring**:
- **Low risk**: Proven tech, clear demand, sufficient resources, flexible timing
- **Medium risk**: Some new tech, moderate demand, some resource constraints
- **High risk**: Experimental tech, uncertain demand, resource constraints, time-sensitive

### 5. Cost of Not Doing

**Questions**:
- Will competitors do this? If yes, when?
- Will users leave if we don't build this?
- Does this get more expensive later? (Technical debt, missed market window)
- Is this blocking other features?

**Scoring**:
- **High cost**: Competitors have it, users leaving, gets harder later, blocking
- **Medium cost**: Competitors might add, some user frustration, minor blocking
- **Low cost**: No competitive pressure, minimal user impact, not blocking

## Prioritization Methods

### Method 1: RICE Scoring

**Formula**:
```
RICE Score = (Reach × Impact × Confidence) ÷ Effort
```

**Reach** (How many users per time period?):
- Example: 1000 users/month
- Example: 50% of user base
- Be specific: Use real numbers

**Impact** (How much impact per user?):
- **3 = Massive impact**: Transformative change
- **2 = High impact**: Significant improvement
- **1 = Medium impact**: Noticeable improvement
- **0.5 = Low impact**: Minor improvement
- **0.25 = Minimal impact**: Barely noticeable

**Confidence** (% How sure are you?):
- **100%**: Hard data, direct measurement
- **80%**: Strong validation, some data
- **50%**: Informed estimate, some validation
- **<50%**: Guess, little validation

**Effort** (Person-months of work):
- Count all work: Product, Design, Engineering, QA, Deployment
- Example: 2 person-months

**Example calculation**:
```
Feature: User search
Reach: 5000 users/month
Impact: 2 (High - helps users find content)
Confidence: 80% (Have search request data)
Effort: 1 person-month

RICE = (5000 × 2 × 0.8) ÷ 1 = 8000
```

### Method 2: MoSCoW Analysis

**Must Have (MVP core)**:
- Not doing this = product cannot function
- Example: User registration for a social app
- Example: Payment for an e-commerce app
- Criteria: Blocks core user journey

**Should Have (Important but not critical)**:
- Important features users expect
- Can be v2 if absolutely necessary
- Example: Password reset (users can request support)
- Example: Search (users can browse)
- Criteria: Significant pain if missing, but not blocking

**Could Have (Nice to have)**:
- Desirable but not necessary
- Do if resources permit
- Example: Dark mode
- Example: Advanced filters
- Criteria: Low pain if missing

**Won't Have (Explicitly not doing)**:
- Out of scope for this product/release
- Document why
- Example: Voice commands (wrong market fit)
- Example: Real-time sync (too expensive)
- Criteria: Doesn't align with strategy/goals

**Rule**: Must Have should be ≤30% of total features. If everything is Must, nothing is.

## Output Format

```markdown
# Priority & Roadmap: [Project/Product]

## Requirements Evaluation

| Feature | User Value | Business Value | Cost | Risk | Cost of Not Doing | RICE | Rank |
|---------|------------|----------------|------|------|-------------------|------|------|
| Feature A | High (10) | High (10) | Medium (2w) | Low | High | 1200 | 1 |
| Feature B | Medium (5) | High (10) | Low (1w) | Medium | Medium | 800 | 2 |
| Feature C | High (10) | Medium (5) | High (2mo) | High | Low | 150 | 3 |

**RICE calculation shown for top 3 features**

## Recommended MVP

### Phase 1 - Core Value (X weeks)
**Focus**: Deliver minimum viable product that solves core problem

- [ ] **Feature A** (Rank 1)
  - Rationale: [Why it's in MVP]
  - Success metric: [How we measure it works]

- [ ] **Feature B** (Rank 2)
  - Rationale: [Why it's in MVP]
  - Success metric: [How we measure it works]

**Total effort**: X weeks

### Phase 2 - Enhancement (Y weeks)
**Focus**: Improve experience and add important missing pieces

- [ ] **Feature C** (Rank 3)
  - Rationale: [Why it's Phase 2]
  - Dependencies: [What must be done first]

- [ ] **Feature D** (Rank 4)
  - Rationale: [Why it's Phase 2]

**Total effort**: Y weeks

### Phase 3 - Expansion (Z weeks) [Deferred]
**Focus**: Extend capabilities after core is proven

- [ ] **Feature E** (Rank 7)
  - Rationale: [Nice to have, low priority]

**Total effort**: Z weeks

## Not Doing & Why

❌ **Feature X** (Original rank Y)
- **Reason**: [Why not doing]
  - [Business reason: Low ROI, wrong market, etc.]
  - [Technical reason: Too expensive, not feasible, etc.]
  - [Strategic reason: Doesn't align with goals]
- **Revisit**: [If ever: Q4/Next year/Never]

❌ **Feature Y** (Original rank Z)
- **Reason**: [Why not doing]
- **Alternative**: [What users can do instead]

## Roadmap Visualization

```
Q1          Q2          Q3          Q4
|-----------|-----------|-----------|-----------|
Phase 1     Phase 2     Phase 3     [New]
(核心)      (增强)      (扩展)      Features
```

## Key Assumptions

For each phase, document assumptions:

1. **Assumption**: [Assumption description]
   - **Validation**: [How we'll validate it]
   - **Timeline**: [When we'll know]
   - **If wrong**: [What we'll do instead]

## Decision Rationale

**Prioritization principles used**:
1. Value-first: Highest ROI features first
2. Risk-averse: Low-risk features before high-risk
3. Fast validation: Quick wins to learn
4. Resource reality: Respect team capacity

**Trade-offs made**:
- Traded [Feature X] for [Feature Y] because [reason]
- Delayed [Feature Z] to Phase 2 because [reason]
- Cut [Feature W] entirely because [reason]
```

## Common Pitfalls

❌ **Everything is P0** → Prioritization fails
- Fix: Force rank everything. If tied, choose based on risk/cost.

❌ **Ignoring opportunity cost** → "Yes to everything"
- Fix: Explicitly state what you're NOT doing.

❌ **Value without cost** → High value, high effort wins
- Fix: Always consider ROI (value ÷ cost).

❌ **Ignoring risk** → High-risk features prioritized
- Fix: Risk-adjust prioritization. De-risk before committing.

❌ **No "won't do" list** → Scope creep
- Fix: Explicitly document what you're not doing and why.

❌ **Ranking by gut feel** → Political prioritization
- Fix: Use RICE or MoSCoW with evidence.

## Example Scenarios

### Example 1: E-commerce MVP

**Features to prioritize**:
1. User registration
2. Product catalog
3. Shopping cart
4. Checkout/payment
5. Order history
6. Product reviews
7. Wishlist
8. Social sharing
9. Product recommendations (AI)
10. Dark mode

**MoSCoW analysis**:
- **Must Have**: 2, 3, 4 (Core transaction: Browse → Cart → Buy)
- **Should Have**: 1, 5 (Expected features: Login, Order history)
- **Could Have**: 6, 7 (Nice to have: Reviews, Wishlist)
- **Won't Have**: 8, 9, 10 (Out of scope: Social, AI, Dark mode)

**MVP (Phase 1)**: Catalog + Cart + Checkout = 4 weeks
**Phase 2**: Add User + Order History = 2 weeks
**Phase 3**: Add Reviews + Wishlist = 2 weeks

### Example 2: SaaS Dashboard

**Features with RICE scores**:

| Feature | Reach | Impact | Confidence | Effort | RICE |
|---------|-------|--------|------------|--------|------|
| Real-time data | 1000 | 2 | 80% | 2mo | 800 |
| Export to CSV | 5000 | 1 | 100% | 0.5mo | 10000 |
| Custom reports | 2000 | 2 | 50% | 3mo | 667 |
| Alerts | 3000 | 1 | 80% | 1mo | 2400 |

**Priority order**:
1. Export to CSV (RICE 10000) - High reach, easy to build
2. Alerts (RICE 2400) - Medium reach, medium effort
3. Real-time data (RICE 800) - High value but very expensive
4. Custom reports (RICE 667) - Medium value, very expensive, uncertain

**MVP**: Export + Alerts = 6 weeks
**Phase 2**: Real-time data = 8 weeks (if Phase 1 validates demand)
**Won't do**: Custom reports (too expensive, uncertain, can start with simpler solution)

## When to Use This Skill

Trigger this skill when:
1. Planning a new product or major feature
2. Resource constraints require trade-offs
3. Determining MVP scope
4. Creating quarterly or annual roadmaps
5. Reassessing priorities based on new information
6. Multiple stakeholders disagree on priorities

## Output Language

Generate prioritization output in Chinese for Chinese-speaking teams.

## Exit Criteria

Prioritization is complete when:
- All features are ranked (no ties)
- RICE or MoSCoW scores calculated for all features
- MVP scope is clearly defined
- "Won't do" list is explicit with rationale
- Roadmap has clear phases with timelines
- Key assumptions are documented
- Trade-offs are stated explicitly
