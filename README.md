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
>>>>>>> adb131af6819f7210199e933cb28de463b93c7d9

---

## Reproduction Process

### Environment Setup

I cloned my fork of the OpenRange repository and followed the current Quick Start instructions from the README as a first-time user on Windows. The main setup path used uv, so I checked that uv was available, ran the dependency setup, and then ran the OpenRange demo command.

The main commands I used were:

uv sync
uv run openrange --help
uv run openrange-demo

The local setup worked successfully. I was able to run the OpenRange demo without setting up Docker, Kind, Helm, or a live infrastructure environment.

### Steps to Reproduce

1. Clone the OpenRange repository.
2. Open the project README.
3. Start from the Quick Start section.
4. Run uv sync to install/sync the project dependencies.
5. Run uv run openrange --help to confirm the CLI is available.
6. Run uv run openrange-demo to try the offline demo.
7. Observe the output and determine whether a newcomer would understand that the demo ran successfully.

### Reproduction Evidence

- **Commit showing reproduction:** https://github.com/LuvAlien/open-range
- **Screenshots/logs:** I ran the Quick Start demo locally using:
                        uv run openrange-demo
                        
                        Output:
                        
                        world=enterprise_saas_v1-1101
                        snapshot=enterprise_saas_v1-1101-10565934
                        winner=blue done=True turns=6
                        red_reward=-0.83 blue_reward=1.2
- **My findings:**
  I was able to run the OpenRange demo locally, which confirms that the project can be tried through the existing Quick Start path.  However, from a newcomer perspective, the README could be improved by explaining prerequisites, what uv is, what successful output looks like, and what the demo output values mean. The current output proves the demo worked, but a new user may not immediately understand what world, snapshot, winner, turns, red_reward, and blue_reward represent.

---

## Solution Approach

### Analysis

The root cause is not that OpenRange fails to run. I was able to run the Quick Start demo locally using uv run openrange-demo, and the command produced a successful world, snapshot, winner, turn count, and reward output.

The issue is that the newcomer experience could be clearer. The README provides working commands, but it does not fully explain what tools are required before running them, what successful output should look like, or what the output values mean. It also includes more advanced infrastructure concepts, which can make the fastest offline demo path less obvious for a first-time user.

### Proposed Solution

I plan to improve the README by making the quickest newcomer path easier to follow. The fix will focus on documentation first: clarifying prerequisites, highlighting the fastest offline demo command, showing expected output, and briefly explaining what the demo output means. This should help a newcomer try OpenRange in around 10 minutes and know whether they ran it successfully.

### Implementation Plan

Using UMPIRE framework (adapted):

**Understand:** [Restate the problem]
The issue is that newcomers need a clearer and faster path to try OpenRange. The offline demo works, but the README should better explain how to get started, what command to run first, and how to understand the output.

**Match:** [What similar patterns/solutions exist in the codebase?]
I will review the current README, Quick Start section, demo command, and related documentation files to match the project’s existing documentation style. I will also compare how the README currently separates offline demo usage from live infrastructure setup.

**Plan:** [Step-by-step implementation plan]
1. Update README.md to make the fastest offline demo path easier to find.
2. Add or clarify prerequisites such as Python and uv.
3. Add the main offline demo command: uv run openrange-demo.
4. Add an example of successful demo output.
5. Explain the meaning of output fields such as world, snapshot, winner, turns, red_reward, and blue_reward.
6. Clarify the difference between the offline demo path and more advanced live/Kind-backed setup if needed.
7. Re-run the Quick Start commands to verify the updated documentation still matches the actual project behavior.

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
I will keep the change focused on newcomer documentation and avoid unrelated code changes. Before opening a pull request, I will review the project’s README style and any contribution guidelines to make sure my changes match the project’s expectations.
**Evaluate:** [How will you verify it works?]
I will verify the change by following the updated Quick Start steps from the perspective of a new user. The documentation will be considered improved if a newcomer can understand what to install, what command to run, what output to expect, and how to know the demo worked.
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
<<<<<<< HEAD
- [GitHub issues or discussions that helped]
=======
- [GitHub issues or discussions that helped]

