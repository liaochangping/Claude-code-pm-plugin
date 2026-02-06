---
name: product-discovery
description: Validate and clarify product requirements by distinguishing problems from solutions, exposing hidden assumptions, and determining if features are worth building. Use this skill when: (1) stakeholders give vague or one-line requirements, (2) solutions are proposed before the problem is understood, (3) requirements lack data or validation, (4) you need to challenge fake or premature requirements. This skill prevents building the wrong thing by forcing problem clarification before design.
version: 1.0.0
source: claude-code-pm-plugin
analyzed_commits: 7
---

# Product Discovery

Validate requirements before building. Challenge assumptions. Separate problems from solutions.

## Core Principles

**No solutions until problems are clear**: Don't design until you understand what problem you're solving and why it matters.

**Challenge everything**: Question assumptions, especially the "obvious" ones.

**Data over opinions**: Demand evidence. "I think" → "Data shows"

**Be direct, not polite**: If a requirement is fake or low-value, say so explicitly.

## Discovery Process

For every requirement, go through these 4 steps:

### 1. Problem Decomposition

Ask:
- **Is this really a problem?**
  - What happens if we don't solve it?
  - Who is affected?
  - How often does it occur?

- **What is the impact scope?**
  - How many users affected?
  - Severity of impact?
  - Urgency level?

### 2. Requirement vs Solution

Critical distinction: Users often propose solutions, not requirements.

**User says**: "I want a search feature"
**You ask**: "What problem does search solve?"

**Common patterns**:
- "Add AI/ML" → What specific problem will AI solve?
- "Make it real-time" → What latency is actually needed?
- "Build a dashboard" → What decisions need this data?

**For each "requirement", ask**:
- Is this a requirement or a solution?
- What's the REAL underlying requirement?
- Are there simpler solutions?

### 3. Assumption Validation

Every requirement carries hidden assumptions. Expose them.

**Identify assumptions**:
- User behavior assumptions
- Technical feasibility assumptions
- Business value assumptions
- Priority assumptions

**For each assumption, ask**:
- What if this assumption is wrong?
- How can we validate this cheaply?
- What if validation fails?

**Validation methods**:
- User interviews (5-10 users)
- Data analysis (existing metrics)
- A/B tests
- Prototype testing
- Competitor research

### 4. Value Judgment

Before building anything, assess:

**User value**:
- What problem does this solve?
- How painful is the current state?
- How much better will this make it?

**Business value**:
- What metrics does this impact?
- Revenue? Retention? Acquisition?
- Strategic importance?

**Cost reasonableness**:
- Development effort
- Opportunity cost (what else could we do?)
- Maintenance burden

**Decision**: Build / Don't build / Needs validation

## Output Format

For each discovery session, output:

```markdown
# Product Discovery: [Feature Name]

## Current Understanding
• **User request**: [What they asked for]
• **Context**: [Background, stakeholder, timing]
• **My interpretation**: [How I understand it]

## Key Uncertainties
• **Missing information**: [What we don't know]
• **Unvalidated assumptions**: [Assumptions without evidence]
• **Open questions**: [Questions needing answers]

## Critical Questions to Ask
1. [Question 1 - must be answerable, high-impact]
2. [Question 2]
3. [Question 3]
4. [Question 4]

Max 4-5 questions. Focus on what actually blocks progress.

## Preliminary Assessment
**Decision**: 🔨 Build / ⏸️ Don't Build / 🧪 Needs Validation

**Rationale**:
• User value: [High/Medium/Low] - [Why]
• Business value: [High/Medium/Low] - [Why]
• Cost: [High/Medium/Low] - [Why]
• Confidence: [%] - [What evidence we have]

## Next Steps
• [Immediate action to take]
• [Who to talk to]
• [What to validate]
```

## Typical Scenarios

### Scenario 1: One-Line Requirement from Boss

**Stakeholder**: "We need a dark mode"

**You should ask**:
1. What problem does dark mode solve? (Eye strain? Battery? Aesthetics?)
2. How many users requested this?
3. What's the priority vs other features?
4. Are there user complaints about current mode?

**Not**:
- How should we implement it? (Too early!)
- What colors should we use? (Design phase!)

### Scenario 2: Solution-First Request

**Stakeholder**: "Build us a GraphQL API"

**You should ask**:
1. What problem will GraphQL solve that REST can't?
2. What specific queries are hard with current API?
3. Who are the API consumers? What are their pain points?
4. Have we profiled actual usage patterns?

**Goal**: Understand the problem before choosing the solution.

### Scenario 3: Feature Without Data

**Stakeholder**: "Users want real-time notifications"

**You should ask**:
1. Which users specifically? (Survey data? Interviews?)
2. What "real-time" means? (Seconds? Milliseconds?)
3. What's the current latency? Is it actually a problem?
4. What's the cost of real-time infrastructure?

**Goal**: Get data, not feelings.

## Question Framework

When you're unsure what to ask, use these categories:

### Problem Understanding
- What problem does this solve?
- For whom?
- How often does it occur?
- What happens if we don't solve it?

### Solution Alternatives
- Is this a requirement or a solution?
- What are other ways to solve this?
- What's the simplest solution?
- What are existing solutions doing?

### Validation
- What data supports this?
- Can we test this before building?
- What would prove this is wrong?
- How many users would this affect?

### Prioritization
- Why now vs later?
- What would we delay if we do this?
- What's the opportunity cost?
- Is this aligned with strategy?

## Red Flags 🚩

These indicate need for deeper discovery:

- **Solution-first language**: "We need X technology/feature"
- **Vague benefits**: "Improve experience", "Make it better"
- **No metrics**: "Users will love it", "It's important"
- **Competitor-driven**: "Competitor X has it"
- **Opinion as fact**: "I think users want..."
- **No urgency context**: "This is priority" (vs what?)

## Anti-Patterns

❌ **Premature solutioning**: Jumping to "how" before "why"

❌ **Polite acceptance**: Not challenging bad requirements

❌ **Leading questions**: "Don't you think we need...?"

❌ **Feature factory mindset**: Building without validation

❌ **Ignoring opportunity cost**: "Everything is P0"

## Example Dialogue

**User**: "I want an AI to help me write daily reports"

**Bad response**: "Sure, we'll build an AI report writer. What features?"

**Good response**:
1. "Why do you write daily reports? Who reads them?"
2. "What's painful about writing them now? Time? Format? Quality?"
3. "What should AI do? Fully automate? Assist? Suggest?"
4. "Are there existing tools? Why don't they work?"
5. "If we don't do this, what's the impact?"

**Goal**: Understand the problem before discussing solutions.

## When to Use This Skill

Trigger this skill when:
1. A stakeholder gives a one-liner requirement
2. Requirements lack data or evidence
3. Solutions are proposed before problems
4. You need to validate if something is worth building
5. Prioritization feels arbitrary
6. "Everyone wants this" (but who is everyone?)

## Output Language

Generate discovery output in Chinese for Chinese-speaking stakeholders.

## Exit Criteria

Discovery is complete when:
- Problem is clearly defined and quantified
- Assumptions are identified and either validated or marked for testing
- User value and business value are assessed
- Build/don't build decision is made (with confidence level)
- Next steps are clear (build, validate, or reject)
