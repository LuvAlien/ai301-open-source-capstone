# Contribution 3: Wording too close together for heading

**Contribution Number:** 3
**Student:** Jacob Webb
**Issue:** https://github.com/robby5000/buttons-rescue/issues/18
**Status:** Phase I Complete

---

## Why I Chose This Issue

I chose this issue because it is a focused visual/UI bug with a clear expected improvement. The issue states that the heading text, “A calm companion with a curious streak,” appears too close together and should be more spaced out. Since this is a visible design issue, it should be realistic to reproduce, inspect, adjust, and verify manually in the browser.

This issue also fits my current learning goals for AI301 because it allows me to continue working in the same `buttons-rescue` repository while treating this as a separate contribution. My previous selected issue in this repo was closed, so this gives me a new active issue where I can practice the full open-source contribution process: understanding the issue, reproducing it locally, identifying the relevant HTML/CSS, making a focused change, and documenting the work clearly.

---

## Understanding the Issue

### Problem Description

The heading text “A calm companion with a curious streak” appears too close together visually. This makes the heading feel cramped and less readable than intended. The issue is asking for the wording to be spaced out more so the design looks cleaner and more polished.

### Expected Behavior

The heading should have better spacing so that “A calm companion with a curious streak” is easier to read and visually balanced within the page layout.

### Current Behavior

The heading currently appears too compressed or too close together. The text spacing does not look visually comfortable and may need adjustment through styling such as line height, letter spacing, margin, padding, or layout spacing.

### Affected Components

The affected component is likely the section of the static homepage that renders the heading “A calm companion with a curious streak.” Since the project appears to be a static website, the affected files will likely include `index.html` and possibly the project’s CSS file. I will identify the exact file, class, and line numbers during Phase II after reproducing the issue locally.

---

## Reproduction Process

### Environment Setup

I updated my local `buttons-rescue` fork to match the current upstream version of the repository, then created a new working branch for issue #18.

* **Repository:** https://github.com/LuvAlien/buttons-rescue
* **Working branch:** https://github.com/LuvAlien/buttons-rescue/tree/fix-heading-spacing
* **Original issue:** https://github.com/robby5000/buttons-rescue/issues/18

Since this project is a static website, I reproduced the issue by opening the `index.html` file directly in the browser:

```powershell
start index.html
```

I also reviewed the codebase manually and located the affected heading in `index.html` inside the `story-copy` section:

```html
<div class="story-copy">
  <h2 id="story-title">A calm companion with a curious streak.</h2>
  <p>Buttons likes gentle company, window watching, and naps that last until dinner. He takes a little time to trust, but once he does, he will follow you from room to room and settle close by.</p>
  <p>He would thrive in a peaceful home with someone who understands that the best friendships are never rushed.</p>
</div>
```

### Steps to Reproduce

1. Open the `buttons-rescue` project locally.
2. Open `index.html` in the browser.
3. Scroll to the “His Story” section.
4. Locate the heading: “A calm companion with a curious streak.”
5. Observe that the heading text appears visually too close together and cramped.
6. Inspect the related markup in `index.html` to identify the affected heading.

### Reproduction Evidence

* **Branch link:** https://github.com/LuvAlien/buttons-rescue/tree/fix-heading-spacing
* **Screenshot:** I captured a screenshot showing the “His Story” section where the heading “A calm companion with a curious streak” appears compressed.
* **My findings:** The issue is reproducible locally. The affected heading is rendered in the `story-copy` section of `index.html` using the `h2` element with the ID `story-title`.

---

## Solution Approach

### Analysis

The issue appears to be a visual spacing problem with the heading text in the “His Story” section. The heading is large and wraps across multiple lines, but the spacing between the words and/or lines appears too tight. This makes the heading look cramped and less readable.

The affected markup is:

```html
<h2 id="story-title">A calm companion with a curious streak.</h2>
```

Since the heading uses the `id="story-title"`, the fix will likely involve locating the CSS rule for `#story-title` or the related `.story-copy h2` styling and adjusting the spacing. The most likely CSS properties involved are `line-height`, `letter-spacing`, `word-spacing`, `max-width`, or related layout spacing.

### Proposed Solution

I plan to improve the visual spacing of the heading by adjusting the CSS that controls the `story-title` heading. I will keep the change focused on the heading spacing issue and avoid changing unrelated content or layout sections.

The likely solution is to increase the heading’s spacing using one or more of the following, depending on the existing CSS:

* `line-height`
* `letter-spacing`
* `word-spacing`
* margin or spacing around the heading
* width/max-width if the text wrapping is causing the cramped appearance

### Implementation Plan

Using UMPIRE framework:

**Understand:**
The “His Story” heading currently reads “A calm companion with a curious streak,” but the wording appears too close together visually. The expected behavior is for the heading to have cleaner spacing and better readability.

**Match:**
I will inspect the existing CSS for `#story-title`, `.story-copy`, and other large headings in the project to understand the design style already being used. I will match the project’s existing visual style instead of introducing a major design change.

**Plan:**

1. Open `index.html` locally and reproduce the spacing issue.
2. Locate the affected heading in `index.html`.
3. Search the CSS file for `#story-title`, `.story-copy`, or related heading styles.
4. Identify which CSS property is causing the heading to appear cramped.
5. Make a small focused spacing adjustment.
6. Refresh the local page and compare the heading before and after the change.
7. Check that the update does not negatively affect nearby paragraphs or the overall layout.
8. Capture an updated screenshot after the fix.

**Implement:**
Branch: https://github.com/LuvAlien/buttons-rescue/tree/fix-heading-spacing

**Review:**
I will review the Git diff before committing to make sure the change only affects the heading spacing issue. I will avoid unrelated formatting, text, or layout changes.

**Evaluate:**
I will manually verify the fix by reopening `index.html` in the browser and confirming that the “A calm companion with a curious streak” heading has improved spacing while the rest of the “His Story” section still looks correct.

---

## Testing Strategy

### Unit Tests

* [ ] Not applicable because this issue is a static visual styling issue.

### Integration Tests

* [ ] Not applicable unless the project includes an existing UI or visual regression test workflow.

### Manual Testing

I will manually test the fix by:

1. Opening `index.html` locally in the browser.
2. Navigating to the “His Story” section.
3. Confirming that the heading “A calm companion with a curious streak” has improved spacing.
4. Checking that the paragraph text below the heading is still aligned and readable.
5. Checking that the design still looks consistent with the rest of the page.
6. Taking a screenshot after the fix as evidence.

---

## Implementation Notes

### Week 1 Progress

I selected this issue after my previous selected `buttons-rescue` issue was closed by the maintainer. Since this new issue is in the same repository, I do not need to refork the project. I created this as Contribution 3 so that the previous contribution remains documented separately.

### Code Changes

* **Files modified:** TBD
* **Key commits:** TBD
* **Approach decisions:** TBD

---

## Pull Request

**PR Link:** TBD

**PR Description:** TBD

**Maintainer Feedback:**

* TBD

**Status:** Not submitted yet.

---

## Learnings & Reflections

### Technical Skills Gained

TBD

### Challenges Overcome

TBD

### What I'd Do Differently Next Time

TBD

---

## Resources Used

* GitHub issue: https://github.com/robby5000/buttons-rescue/issues/18
* Repository: https://github.com/robby5000/buttons-rescue
