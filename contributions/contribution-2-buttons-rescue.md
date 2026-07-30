# Contribution [#]: [Issue Title]

**Contribution Number:** [ 2 ]  
**Student:** [Jacob Webb]  
**Issue:** [https://github.com/robby5000/buttons-rescue/issues/21]
**Status:** Phase 1 Complete

---

## Why I Chose This Issue

I chose this issue because it is a focused UI/content bug with a clear expected result. The issue describes that the “Bring Buttons Home” section is displaying numbers in the order 1, 3, 2, when they should appear in the correct order as 1, 2, 3. Since the problem is specific and visible in the interface, it should be realistic to reproduce, investigate, and verify.

This issue also matches my current learning goals for AI301 because it gives me a manageable first open-source contribution. I can practice forking a real project, setting up the local environment, locating the relevant UI/component code, making a small focused fix, and documenting my work clearly through the contribution process.
---

## Understanding the Issue

### Problem Description

The “Bring Buttons Home” section appears to have its numbered items displayed out of order. Instead of showing the steps in sequence, the section currently shows them as 1, 3, 2.

### Expected Behavior

The “Bring Buttons Home” section should display the numbered items in the correct order: 1, 2, 3.

### Current Behavior

The section currently displays the numbered items as 1, 3, 2, which makes the sequence appear incorrect or confusing to users.

### Affected Components

The affected component is likely the page or section that renders the “Bring Buttons Home” content. I will identify the exact file/component during Phase II after cloning the project and searching the codebase for the text or section markup.

---

## Reproduction Process

### Environment Setup

I cloned my fork of the buttons-rescue repository and created a working branch for this issue.

Repository: https://github.com/LuvAlien/buttons-rescue
Working branch: https://github.com/LuvAlien/buttons-rescue/tree/fix-bring-buttons-order

To understand the project before making any changes, I reviewed the codebase myself and also used Claude to help explain the structure of the files and identify where the homepage content was being rendered. I used AI as a code-reading assistant, but I verified the issue manually by running the project locally and inspecting the HTML myself.

Since this project is a static website, I reproduced the site locally by opening the index.html file directly in the browser:

start index.html

### Steps to Reproduce

1. Clone the buttons-rescue repository.
2. Open the project locally in VS Code.
3. Open index.html in the browser using start index.html.
4. Scroll to the “Bring Buttons home” section.
5. Observe the order of the numbered steps.
6. Confirm that the section displays the steps as 01, 03, 02 instead of the expected order 01, 02, 03.

### Reproduction Evidence

- **Commit showing reproduction:** (https://github.com/LuvAlien/buttons-rescue/tree/fix-bring-buttons-order)
- **Screenshots/logs:** I captured a screenshot showing the “Bring Buttons home” section displaying the steps in the incorrect order.
- **My findings:** [What you discovered during reproduction]
The issue is reproducible locally. The page displays:
01 — Talk it over
03 — Come say hello
02 — Apply to adopt

The expected sequence should be:

01 — Talk it over
02 — Apply to adopt
03 — Come say hello

After reviewing the codebase, I located the issue in index.html, around lines 70–85. The problem appears to be caused by the order of the two <li> elements containing the 02 and 03 steps.
---

## Solution Approach

### Analysis

The root cause appears to be that the list items in the “Bring Buttons home” section are written in the wrong order in the HTML. The content for step 03 appears before the content for step 02, which causes the page to display the adoption steps as 01, 03, 02.

This does not appear to require a large logic change or new functionality. The issue is likely a static content ordering bug in the homepage markup.
### Proposed Solution

I plan to fix the issue by switching the order of the two <li> elements that contain the 02 and 03 steps in index.html. After making the change, I will reopen the page locally and confirm that the “Bring Buttons home” section now displays in the correct order: 01, 02, 03.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The “Bring Buttons home” section currently displays the steps out of order. The current order is 01, 03, 02, but the expected order is 01, 02, 03.

**Match:** I reviewed the homepage structure and found that this section is rendered directly in index.html. Since the numbered steps are static HTML list items, the fix should follow the existing markup style instead of introducing new logic.

*Plan:** [Step-by-step implementation plan]
1. Open index.html.
2. Locate the “Bring Buttons home” section around lines 70–85.
3. Identify the <li> element for step 02.
4. Identify the <li> element for step 03.
5. Move the step 02 list item above the step 03 list item.
6. Save the file.
7. Reopen or refresh index.html in the browser.
8. Verify that the section now displays 01, 02, 03.
9. Check that the layout, spacing, and text still look correct after the change.

**Implement:** Branch: https://github.com/LuvAlien/buttons-rescue/tree/fix-bring-buttons-order

**Review:** I will review the diff before committing to make sure the only change is the ordering of the affected list items. I will avoid changing unrelated formatting, styling, or content.

**Evaluate:** I will manually test the fix by reopening the local index.html page and confirming that the “Bring Buttons home” section displays in the correct order. I will compare the page visually before and after the change to make sure the issue is resolved without breaking the design.

---

## Testing Strategy

### Unit Tests

Not applicable at this stage because the issue appears to be a static HTML ordering bug and the project does not appear to require a unit test for this content change.

### Integration Tests

Not applicable at this stage unless the project has an existing automated UI/page test workflow.

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
