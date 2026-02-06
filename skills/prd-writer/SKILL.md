---
name: engineering-prd-writer
description: Generate engineering-ready Product Requirement Documents (PRDs) with clear acceptance criteria, edge cases, and implementation details. Use this skill when writing PRDs for software features that will be implemented by engineering teams. This skill produces PRDs that are: (1) implementation-focused with technical details, (2) unambiguous with explicit boundaries, (3) testable with Given-When-Then acceptance criteria, and (4) directly decomposable into development tasks.
version: 1.0.0
source: claude-code-pm-plugin
analyzed_commits: 7
---

# Engineering PRD Writer

Generate PRDs that engineering teams can actually implement - no fluff, no ambiguity.

## Core Principles

**Engineering-first PRDs**: Every section must serve implementation. If it doesn't help engineers build, test, or verify, remove it.

**Quantifiable success**: All goals must be measurable. "Improve user experience" → "Reduce page load time from 3s to 1s"

**Explicit boundaries**: Clearly state what's NOT being done and why.

**Edge case coverage**: Exception flows are as important as happy paths.

## PRD Structure

Write PRDs in this exact order with these 8 mandatory sections:

### 1. Background & Goals

**Background** (why now):
- Current problem
- User feedback/data
- Business context

**Goals** (measurable outcomes):
```
• Metric 1: From X to Y (e.g., Daily active users +20%)
• Metric 2: Reduce/Increase Z by N%
• Metric 3: Achieve specific target
```

### 2. User Roles & Core Scenarios

- **Target users**: Who (specific personas)
- **Usage scenarios**: When, where, what they're doing
- **Core pain points**: Current problems

### 3. Feature Scope

**In Scope** (we WILL do):
- Feature 1: Brief description
- Feature 2: Brief description

**Out of Scope** (we will NOT do - and why):
- Feature A (Reason: technical limitation/low priority/outside scope)
- Feature B (Reason: defers to Phase 2)

**Critical**: Being explicit about what you're NOT doing prevents scope creep.

### 4. Detailed Flows

**Happy Path** (normal flow):
```
Step 1: User action → System response
Step 2: User action → System response
```

**Exception Paths** (MUST include):
- Network failure handling
- Data validation failures
- Insufficient permissions
- Edge cases (empty states, boundary values, concurrent operations)
- Error recovery flows

**Rule**: For every user action, define what happens when it fails.

### 5. Interaction Specification

Describe UI/UX behavior in text (no mockups required):
- Page navigation logic
- Button state changes (enabled/disabled/loading)
- Loading states (spinners, skeletons, progress bars)
- Error messages (specific text for each error type)
- Success feedback (toasts, banners, redirects)

### 6. Data & Analytics

**Data Fields** (table format):
```
| Field | Type | Description | Required |
|-------|------|-------------|----------|
| ...   | ...  | ...         | ...      |
```

**Analytics Events** (table format):
```
| Event Name | Trigger | Parameters | Priority |
|------------|---------|------------|----------|
| ...        | ...     | ...        | P0/P1/P2 |
```

**Priority levels**:
- P0: Critical for business (must track)
- P1: Important (should track)
- P2: Nice to have (track if feasible)

### 7. Acceptance Criteria

Use **Given-When-Then** format for testable criteria:

```
AC-1: [Feature name]
Given: [Precondition]
When: [User action]
Then: [Observable result]

AC-2: [Edge case]
Given: [Precondition]
When: [Action that would normally fail]
Then: [Graceful error handling]
```

**Rule**: Every feature must have at least one AC. Every edge case must have an AC.

### 8. Risks & Dependencies

**Risks**:
- Technical risks (implementation challenges)
- Business risks (user adoption, revenue impact)
- Operational risks (performance, scalability)

**Dependencies**:
- External systems/APIs
- Other teams
- Infrastructure changes
- Data migrations

## Writing Guidelines

### Be Specific, Not Vague

❌ **Avoid**: "Optimize performance", "Improve UX", "Enhance experience"

✅ **Use**: "Reduce API response time from 500ms to <200ms", "Reduce form fields from 10 to 5", "Add one-click purchase"

### Define Boundaries Explicitly

Always answer:
- What's IN scope?
- What's OUT of scope?
- Why?

### Cover Edge Cases

For each feature, ask:
- What if the network fails?
- What if the user has no data?
- What if multiple users act simultaneously?
- What if the data is corrupted?
- What if the external API is down?

### Make Every Feature Testable

If you can't write an acceptance criterion for it, it's not well-defined.

## Common Anti-Patterns

❌ **Writing implementation details in the PRD**
- Exception: When technical constraints affect user experience

❌ **Being "polite" about what's not included**
- Be explicit: "We're not doing X because Y"

❌ **Only documenting happy paths**
- Exception flows are where bugs live

❌ **Using business jargon engineers don't understand**
- Translate: "User engagement" → "Daily active users"

## PRD Template

```markdown
# [Feature Name] PRD

## 1. Background & Goals
### Background
• Current problem: ...
• User feedback: ...

### Goals
• Metric 1: From X to Y
• Metric 2: Reduce Z by N%

## 2. User Roles & Core Scenarios
• Target users: ...
• Core scenarios: ...

## 3. Feature Scope
### In Scope
• Feature 1
• Feature 2

### Out of Scope
• Feature A (Reason: ...)
• Feature B (Reason: ...)

## 4. Detailed Flows
### Happy Path
• Step 1: ...
• Step 2: ...

### Exception Paths
• Network failure: ...
• Validation error: ...
• Permission denied: ...

## 5. Interaction Specification
• Page navigation: ...
• Button states: ...
• Loading states: ...
• Error messages: ...

## 6. Data & Analytics
### Data Fields
| Field | Type | Description | Required |
|-------|------|-------------|----------|
| ...   | ...  | ...         | ...      |

### Analytics Events
| Event | Trigger | Params | Priority |
|-------|---------|--------|----------|
| ...   | ...     | ...    | ...      |

## 7. Acceptance Criteria
AC-1: ...
Given: ...
When: ...
Then: ...

AC-2: ...
Given: ...
When: ...
Then: ...

## 8. Risks & Dependencies
### Risks
• ...

### Dependencies
• ...
```

## When to Use This Skill

Trigger this skill when:
1. Writing a PRD for a software feature
2. Converting business requirements into technical specifications
3. Creating documentation for engineering teams to implement
4. Defining acceptance criteria for QA testing
5. Planning feature releases with measurable goals

## Output Format

Generate PRDs as Markdown files with:
- Chinese language (for Chinese-speaking teams)
- Table format for data fields and analytics events
- Code blocks for Given-When-Then acceptance criteria
- Clear section headers (##, ###)
- Bullet points for lists
