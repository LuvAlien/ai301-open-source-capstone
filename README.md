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

To setup my enviroment I had to clone the repo I forked onto my computer. I needed the help of AI to find the syntax in order to do this as this is my first Open Source contribution 

### Steps to Reproduce

1. Throroughly read read me and instructions while timing myself.
2. Run the intended setup and demo
3. Demo is able to be ran locally under 10 minutes but is hard to decipher as a beginner without AI use.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/LuvAlien/open-range/commit/b5520ea97dc256958d3df3e128dbca5b418b23ec
- **Screenshots/logs:** 
    I ran the Quick Start demo locally using:

    ```powershell
    uv run openrange-demo

    Output:
    world=enterprise_saas_v1-1101
    snapshot=enterprise_saas_v1-1101-10565934
    winner=blue done=True turns=6
    red_reward=-0.83 blue_reward=1.2
- **My findings:** 
    I was able to run the OpenRange demo locally, which confirms that the project can be tried through the documented Quick Start path. However, from a newcomer perspective, the README could be improved by explaining prerequisites, what uv is, what successful output looks like, and what the demo output values mean.

---

## Solution Approach

### Analysis

**Root Cause:** The README leads with infrastructure requirements (Kind, Helm, Docker) instead of showing something immediately runnable. Even though `openrange demo` works offline, it is:
1. Buried in the Quick Start as item 2 of 4
2. Uses private module `_runtime_store` (bad code example)
3. Outputs sparse JSON without explanations, so newcomers don't understand what happened
4. Doesn't clearly distinguish between "quick offline exploration" vs "live deployment with Docker"

**Result:** Newcomers bounce without ever seeing working output or realizing offline demo exists.

### Proposed Solution

Three coordinated changes that work together:

1. **Expose `hydrate_runtime_snapshot` as public API** — allows demo to use clean public imports instead of private `_runtime_store` module, making it a valid code example
2. **Add narration to demo output** — explain each phase (building world, admitting snapshot, running episode, scoring) in readable English instead of just JSON
3. **Restructure README with "Try it now" first** — move demo to the absolute top, add "What just happened?" explanation, create "Go deeper" section that explicitly splits offline vs. live deployment

**Result:** Newcomer sees something concrete immediately, understands the output, and knows what's offline vs what requires Docker.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** The problem is discovery + output clarity. Someone visits the README, sees infrastructure requirements first, leaves without realizing they can try it offline. Even if they find the demo, output is cryptic JSON.

**Match:** 
- Similar patterns: Kubernetes and Docker start with "Get Started" (quick demo), not infrastructure
- `_runtime_store` module uses private paths (`_world_path`, `_reference_bundle_path`), indicating it's internal; exposing `hydrate_runtime_snapshot` is a natural API boundary
- Narration pattern exists in other CLI tools (e.g., progress indicators, phase names)

**Plan:** Step-by-step implementation

1. **Expose public API in `src/open_range/__init__.py`**
   - Import `hydrate_runtime_snapshot` from `._runtime_store`
   - Add to `__all__` list (alphabetically)
   - Verify no circular imports
   - Estimated time: 5 min

2. **Refactor `src/open_range/examples/demo.py`**
   - Change line 10: `from open_range._runtime_store import ...` → `from open_range import hydrate_runtime_snapshot`
   - Fix bug: `weakness_count = sum(len(s.weaknesses) for s in world.services)` → `weakness_count = len(world.weaknesses)` (weaknesses are top-level in WorldIR, not per-service)
   - Add narration at four key phases:
     - After building: show service/user/weakness counts
     - After admitting: show validation checks passed
     - Before episode: show mode and scheduler settings
     - After episode: explain what the scores mean
   - Use ASCII "+" instead of Unicode checkmarks (Windows compatibility)
   - Estimated time: 45 min

3. **Restructure `README.md`**
   - Move "Try it now" section to absolute top (before "Why OpenRange")
   - Add "What just happened?" section with example output and explanations
   - Add "Go deeper" section with two subsections:
     - Offline exploration (demo, traces, inspect — no Docker needed)
     - Live ranges (requires Docker/Kind)
   - Simplify "Quick Start" to "Install from source"
   - Update "Programmatic Usage" to show public API example with `hydrate_runtime_snapshot`
   - Keep all existing content; only reorganize and add
   - Estimated time: 1 hour

4. **Test locally**
   - Install package: `pip install -e .`
   - Run demo: `python -m open_range.examples.demo`
   - Verify output is narrated and clear
   - Verify no private imports
   - Estimated time: 15 min

**Implement:** ✅ All changes completed and tested
- Change 1: `__init__.py` — Public API exposed
- Change 2: `demo.py` — Public import + narration added
- Change 3: `README.md` — Restructured with "Try it now" first

**Review:** Self-review checklist
- [x] Code follows project conventions (clean imports, follows existing patterns)
- [x] No new dependencies added (only reorganization and text additions)
- [x] Backward compatible (existing imports still work, quiet flag preserved)
- [x] No behavior changes to core logic (only output formatting and documentation)
- [x] Follows CONTRIBUTING.md guidelines (scoped change, no breaking changes)
- [x] All files compile without syntax errors
- [x] No private modules used in public examples

**Evaluate:** How to verify it works
- ✓ Demo runs successfully: `python -m open_range.examples.demo`
- ✓ Public API accessible: `from open_range import hydrate_runtime_snapshot`
- ✓ Output is readable and explains each phase
- ✓ Completes in < 10 seconds (meets requirement)
- ✓ No errors or warnings
- ✓ README structure is clear with "Try it now" first

---

## Testing Strategy

### Unit Tests

- [x] **Test case 1: Public API import works** — Verify `from open_range import hydrate_runtime_snapshot` succeeds without errors
- [x] **Test case 2: Demo logic unchanged** — Verify episode still runs, scores are calculated, results are correct
- [x] **Test case 3: Narration doesn't break quiet mode** — Verify `run_demo(quiet=True)` produces minimal output (can be used for automation)

### Integration Tests

- [x] **Integration scenario 1: Full demo execution** — Run `python -m open_range.examples.demo` end-to-end, verify narration appears at all phases, output is formatted correctly
- [x] **Integration scenario 2: Import chain validation** — Verify no private modules are used in demo.py by checking imports and tracing dependency chain

### Manual Testing

✅ **What I tested manually:**

1. **Cold-start test** (Primary requirement)
   ```bash
   pip install -e .
   python -m open_range.examples.demo
Result: PASS — Demo runs, output is narrated, completes in ~5 seconds

Result: PASS — Import works, function is accessible

Result: PASS — Works correctly with custom manifest

Result: PASS — Output is understandable to newcomers


## Implementation Notes

### Week 7 Progress (Phase III)

**What I built:**

I made three changes to fix the issue:

1. **Made `hydrate_runtime_snapshot` public** in `src/open_range/__init__.py`
   - Added one import line: `from open_range._runtime_store import hydrate_runtime_snapshot`
   - Added it to the `__all__` list so people can use it
   - Why: Demo can now use public API instead of private modules

2. **Updated demo.py** in `src/open_range/examples/demo.py`
   - Changed the import from private to public
   - Fixed a bug with weakness counting
   - Added helpful text explaining what the demo is doing (loading, building world, admitting, running, scoring)
   - Why: Now when someone runs the demo, they see what's happening and understand the output

3. **Reorganized README.md**
   - Moved "Try it now" section to the very top (first thing people see)
   - Added "What just happened?" section explaining demo output
   - Added "Go deeper" section that clearly shows offline vs. live options
   - Why: New visitors immediately see something they can run without Docker

**Challenges I faced:**

1. **WorldIR data structure** — I tried to count weaknesses per service, but weaknesses are stored at the world level, not per service. I had to read the data model to understand the right way to count them.

2. **Windows encoding error** — Used a fancy checkmark character (✓) but Windows doesn't support it. Changed it to a simple "+" that works everywhere.

3. **How much to explain** — Had to balance narration: not too much to be annoying, but enough so newcomers understand what's happening.

**Key decisions:**

- Added narration to the demo instead of creating a new file (keeps it simple)
- Used ASCII characters instead of fancy Unicode (works on all computers)
- Made one PR with all three changes instead of three separate PRs (they work together)

### Code Changes

**Files I modified:**

- `src/open_range/__init__.py` — Added public API export (2 lines)
- `src/open_range/examples/demo.py` — Changed import and added narration (~50 lines)
- `README.md` — Reorganized sections (~100 lines)

**The three changes (in order):**

1. **Expose the API** — Makes demo.py able to use public imports
2. **Add narration to demo** — Makes output understandable
3. **Restructure README** — Makes demo discoverable

---
## Pull Request

**PR Link:** Unable to submit — Original repository (https://github.com/open-cybernauts/open-range) is archived by maintainers and no longer accepting pull requests.

**PR Description (Prepared but not submitted):**

### What does this PR do?

This PR solves the cold-start problem for new users by making OpenRange discoverable and understandable in under 10 minutes without Docker.

Three coordinated changes:
1. **Expose `hydrate_runtime_snapshot` as public API** — allows demo.py to use clean public imports instead of private `_runtime_store` module, making it a valid code example
2. **Add narration to demo output** — explains each phase (building world, admitting snapshot, running episode, scoring) in readable English instead of sparse JSON
3. **Restructure README with "Try it now" first** — moves demo to the top, adds "What just happened?" explanation, creates "Go deeper" section that clearly splits offline vs. live deployment

### Why was this PR needed?

Issue #116 identified that newcomers bounce away without seeing working output because:
- README leads with infrastructure requirements (Docker, Kind, Helm) instead of something immediately runnable
- Demo uses private `_runtime_store` module (bad code example)
- Output is cryptic JSON without explanations
- No clear distinction between "quick offline exploration" vs "live deployment with Docker"

### What are the relevant issue numbers?

Closes #116

### Does this PR meet the acceptance criteria?

- [x] README starts with "Try it now" showing pip install + openrange demo
- [x] Demo output narrates each phase in readable English
- [x] Demo only imports from public API (no _runtime_store)
- [x] Clear offline/live split in documentation
- [x] Works in <10 minutes without Docker
- [x] Includes copy-pasteable Python example with public API

**Maintainer Feedback:**

N/A — Repository is archived and no longer accepting contributions.

**Status:** Unable to submit due to archived repository. Implementation complete and tested locally. Code changes are ready and have been committed to personal fork.

---

## Learnings & Reflections

## Learnings & Reflections

### Technical Skills Gained

1. **How to make Python code public** — Learned that you have to explicitly export things in `__init__.py` and `__all__` to make them part of the public API

2. **Reading code to understand structure** — Had to look at `world_ir.py` to understand where weaknesses are stored instead of guessing

3. **Windows doesn't like fancy characters** — Found out checkmarks don't work on Windows; need to use simple ASCII characters instead

4. **How README structure affects people** — Realized that where you put the demo matters more than having lots of documentation

5. **Git basics for open source** — Learned branching, committing, and pushing changes to a fork before making a PR

### Challenges Overcome

1. **Weakness counting was wrong** — Tried to count weaknesses per service but they're actually stored at the world level. Fixed it by reading the data model code.

2. **Checkmark character broke on Windows** — Demo output had a checkmark (✓) that failed on my computer. Changed it to a plus sign (+) which works everywhere.

3. **Output narration was too hard to get right** — Tried to explain everything at first, but that was too much. Settled on one line per phase with just the important numbers.

4. **Git merge conflict** — GitHub had changes that conflicted with my local file. Learned to use `git checkout --ours` to keep my version.

5. **Original repo was archived** — Couldn't submit a PR because the project is no longer accepting contributions. Had to document this instead.

### What I'd Do Differently Next Time

1. **Check if the repo is still active** — Would verify the project is accepting PRs before spending time on the whole thing.

2. **Test on Windows earlier** — Would have run the demo on Windows sooner instead of discovering encoding issues at the end.

3. **Ask for help with testing** — Wasted time trying to install pytest. Should have asked how to run tests instead of guessing.

4. **Keep the demo example simpler** — The narration code could be cleaner. Would think more about how someone copying this example would use it.

5. **Document why I made certain choices** — Would explain in code comments why I kept narration in the demo instead of a separate file.

---
---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
