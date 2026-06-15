# Contribution [#]: A newcomer can try OpenRange in 10 minutes
 


**Contribution Number:** 1  
**Student:** Jacob Webb 
**Issue:** (https://github.com/open-cybernauts/open-range/issues/116)  
**Status:** Phase 1 In Progress

---

## Why I Chose This Issue

This issue interest me because the issue involves creating an efficient read me which is a very valuable skill and needed for every github project.

---

## Understanding the Issue

### Problem Description

Introduce user to know that there is both an openrange demo they can try offline and there is also live exploration if they want to implement the project themselves. 

### Expected Behavior

Create a ReadMe explaining what the user must do in order to get the user running in under 10 minutes. Also the demo serves as a working code example users can copy.

### Current Behavior

openrange demo works without Docker — builds a snapshot offline, runs scripted agents in simulated time, prints scores

But README leads with infrastructure requirements (Kind, Helm, Docker)

The demo imports from _runtime_store, a private module — bad example for contributors

Demo output is terse JSON, doesn't explain what's happening

No distinction in docs between "explore offline" and "run live ranges"

### Affected Components

README.md — restructure with "Try it now" at top, clear offline/live split

src/open_range/examples/demo.py — replace _runtime_store import with public API, add narration to output

src/open_range/cli.py — ensure openrange demo subcommand prints readable output

Possibly modified:

src/open_range/__init__.py — if hydrate_runtime_snapshot needs to be exposed publicly (or demo refactored to not need it)

---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]

### Steps to Reproduce

1. [Step 1]
2. [Step 2]
3. [Observed result]

### Reproduction Evidence

- **Commit showing reproduction:** [Link to commit in your fork]
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]

**Match:** [What similar patterns/solutions exist in the codebase?]

**Plan:** [Step-by-step implementation plan]
1. [Modify file X to do Y]
2. [Add function Z]
3. [Update tests]

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
