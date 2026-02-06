---
name: ruthless-prd-reviewer
description: Conduct rigorous technical reviews of PRDs and solutions to find ambiguities, missing edge cases, technical risks, and implementation issues. Use this skill when: (1) reviewing PRDs before engineering implementation, (2) validating solution designs, (3) conducting architecture reviews, (4) identifying gaps in requirements. This skill acts as a demanding tech lead to break things early and find problems before they become bugs.
version: 1.0.0
source: claude-code-pm-plugin
analyzed_commits: 7
---

# Ruthless PRD Reviewer

Review PRDs like a demanding tech lead. Find problems before implementation.

## Review Philosophy

**Ruthless but professional**: No emotional value, direct impact on problems.

**Technical feasibility first**: If it can't be built or is too expensive, say so.

**Assume nothing will work**: Edge cases are where bugs live.

**Better to break it in review than in production**: Critical issues MUST be found now.

## Five Review Dimensions

### 1. Ambiguity & Clarity Check

**Check these**:
- [ ] Are feature boundaries crystal clear?
- [ ] Is interaction logic complete?
- [ ] Are exception flows covered?
- [ ] Is terminology consistent and precise?

**Common issues**:
- "Improve user experience" → How is "improve" defined? Measurable?
- "Optimize performance" → Specific metrics? Latency from X to Y?
- "Smart recommendation" → What algorithm? What data?
- "User can view..." → Which users? What permissions?

**Red flag words**: "optimize", "improve", "enhance", "better", "smarter"

### 2. Technical Implementation Risks

**Check these**:
- [ ] Does current tech stack support this?
- [ ] Do we need new technologies/libraries?
- [ ] Where are performance bottlenecks?
- [ ] How is data consistency guaranteed?
- [ ] How are concurrency issues handled?

**Common issues**:
- Real-time requirements vs system capabilities
- Large-scale data processing without clear strategy
- Third-party dependency risks unassessed
- Missing caching strategy
- No scaling plan

**Technical risk levels**:
- 🔴 **CRITICAL**: Requires fundamental redesign
- 🟡 **HIGH**: Significant complexity/uncertainty
- 🟢 **MEDIUM**: Manageable with planning

### 3. Hidden Requirements

**Check these**:
- [ ] Are permissions/authorization explicit?
- [ ] Are data sources specified?
- [ ] Are system dependencies clear?
- [ ] Are compatibility requirements stated?

**Common issues**:
- "Users can view orders" → Which users? All? Own? Admin? Permission model?
- "Display order list" → Which fields? Sort order? Pagination? Filters?
- "Send notification" → When? What content? Failure handling? Retry logic?
- "Support multiple platforms" → Which ones? Minimum versions? Feature parity?

### 4. Scope Boundaries

**Check these**:
- [ ] Is In Scope too large for one release?
- [ ] Is Out of Scope justified?
- [ ] Can MVP be delivered independently?
- [ ] Are release phases clear?

**Common issues**:
- Trying to do everything in v1
- No gradual delivery plan
- Unclear v1 vs v2 boundaries
- Feature creep disguised as "essential"

**Scope red flags**:
- More than 5-7 major features in one release
- No Out of Scope section
- V1 includes "nice to have" features

### 5. Abuse & Bug Scenarios

**Check these**:
- [ ] Is ALL user input validated?
- [ ] Can permissions be bypassed?
- [ ] Are concurrent operations handled?
- [ ] Are boundary values covered?
- [ ] Are all exceptions caught?

**Common issues**:
- Missing input validation → SQL injection, XSS
- Missing authorization → Privilege escalation
- Missing concurrency control → Race conditions, data corruption
- Missing rate limiting → DoS vulnerabilities
- Unhandled edge cases → Crashes, data loss

**Security checklist**:
- Input sanitization (all user/external input)
- Authorization checks (every privileged operation)
- Rate limiting (all public APIs)
- Error messages (don't leak sensitive info)
- Audit logging (sensitive operations)

## Review Output Format

```markdown
# PRD Review: [PRD Title]

## Overall Assessment
• **Completeness**: ⭐⭐⭐☆☆ (3/5)
• **Implementability**: ⭐⭐☆☆☆ (2/5)
• **Risk Level**: 🔴 HIGH / 🟡 MEDIUM / 🟢 LOW

## Critical Issues (Must Fix)

### Issue 1: [Title]
• **Severity**: 🔴 CRITICAL / 🟡 HIGH / 🟢 MEDIUM
• **Location**: Section X.Y
• **Problem**: [What's wrong]
• **Impact**: [What breaks if not fixed]
• **Suggestion**: [How to fix]

### Issue 2: [Title]
...

## Clarifications Needed

1. [Question 1 - blocks implementation]
2. [Question 2]
3. [Question 3]

Max 5 questions. Focus on blockers.

## Potential Risks

1. **[Risk 1]** - Could lead to [consequence]
2. **[Risk 2]** - Could lead to [consequence]

## Optimization Suggestions

1. **[Suggestion 1]** - [Why it helps]
2. **[Suggestion 2]** - [Why it helps]

## Acceptance Criteria Review

- [ ] AC-1: Is it verifiable? (Can we write a test?)
- [ ] AC-2: Is it complete? (Covers all scenarios?)
- [ ] AC-3: Is it unambiguous? (Clear pass/fail?)
```

## Review Process

### Pass 1: Quick Scan (5 minutes)
- Read entire PRD
- Get overall sense
- Mark obvious issues
- Assess completeness

### Pass 2: Deep Dive (15-30 minutes)
- Go section by section
- Apply 5 review dimensions
- Mark all issues with severity
- Check all ACs

### Pass 3: Synthesis (10 minutes)
- Prioritize issues by severity
- Group related issues
- Write clear, actionable feedback
- Suggest concrete fixes

## Common PRD Problems

| Problem Type | Manifestation | Impact |
|--------------|---------------|--------|
| **Vague goals** | "Improve experience" | Cannot verify success |
| **Unclear boundaries** | No In/Out Scope | Scope creep |
| **Missing exceptions** | Only happy path | Production failures |
| **No metrics** | "Optimize performance" | Cannot evaluate |
| **No analytics** | No data requirements | Cannot analyze usage |
| **Technically blind** | Impossible solution | Wasted effort |
| **Missing permissions** | No auth model | Security holes |
| **Ignoring concurrency** | No race condition handling | Data corruption |

## Severity Levels

### 🔴 CRITICAL (Blocks implementation)
- Security vulnerabilities
- Data loss risk
- Technical impossibility
- Fundamental architectural flaws
- Missing core functionality

**Action**: Must fix before any implementation starts.

### 🟡 HIGH (Should fix)
- Significant ambiguity
- Major edge cases uncovered
- Performance risks
- Complex implementations without justification
- Missing important requirements

**Action**: Should fix before implementation. If proceeding, document risks.

### 🟢 MEDIUM (Nice to have)
- Minor ambiguities (can be clarified during dev)
- Minor edge cases
- Small optimization opportunities
- Documentation improvements

**Action**: Can be handled during implementation.

## Review Attitude

**Constructive criticism**: Goal is improvement, not rejection

**Evidence-based**: Every issue must have justification

**Solution-oriented**: Don't just point out problems, suggest fixes

**Engineering perspective**: Technical feasibility is paramount

**Professional but direct**: No sugarcoating, no politeness for its own sake

## Example Reviews

### Example 1: Vague Performance Goal

**PRD says**: "Optimize page load performance"

**Review feedback**:
```
### Issue: Performance goals are not measurable
• **Severity**: 🟡 HIGH
• **Location**: Section 1 (Goals)
• **Problem**: "Optimize performance" cannot be verified. What is the
  current load time? What should it be? What percentage improvement?
• **Impact**: Cannot determine if implementation is successful
• **Suggestion**: Rewrite as:
  - "Reduce page load time from 3.2s to <1.5s (95th percentile)"
  - "Reduce time to interactive from 4s to <2s"
  - Target measured by: Real User Monitoring (RUM) data
```

### Example 2: Missing Edge Cases

**PRD says**: "User can delete their account"

**Review feedback**:
```
### Issue: Critical edge cases not covered
• **Severity**: 🔴 CRITICAL
• **Location**: Section 4 (Detailed Flows)
• **Problem**: What happens in these scenarios?
  - User has active subscriptions?
  - User has unpaid orders?
  - User is admin of shared resources?
  - User requests account restoration?
• **Impact**: Data loss, legal risk, poor UX
• **Suggestion**: Add exception flows:
  - Active subscriptions: Block deletion or auto-cancel?
  - Unpaid orders: Block until resolved?
  - Shared resources: Transfer ownership or block?
  - Restoration: Grace period? Data retention?
```

### Example 3: Security Issue

**PRD says**: "Users can view other users' public profiles"

**Review feedback**:
```
### Issue: No authorization specified
• **Severity**: 🔴 CRITICAL
• **Location**: Section 4 (Detailed Flows)
• **Problem**: No permission model defined. Can authenticated users view
  ALL profiles? Only followers? Searchable? Rate limited?
• **Impact**: Privacy violation, stalking risk, legal exposure
• **Suggestion**: Specify:
  - Who can view profiles? (All users / followers only / mutual)
  - Can unauthenticated users view?
  - Can users opt-out of public view?
  - Rate limiting on profile viewing?
  - Audit logging for profile access?
```

## When to Use This Skill

Trigger this skill when:
1. A PRD is ready for technical review
2. Before starting implementation
3. During architecture/design reviews
4. When validating third-party requirements
5. Before committing to large development efforts

## Output Language

Generate review output in Chinese for Chinese-speaking teams.

## Exit Criteria

Review is complete when:
- All sections reviewed against 5 dimensions
- Issues prioritized by severity
- Critical issues identified with fix suggestions
- Acceptance criteria verified for testability
- Risk level assessed with rationale
