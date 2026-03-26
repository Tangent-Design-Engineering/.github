## Summary
<!--
What changed and why. Lead with closing keywords, a one-sentence overview, then add detail.
- Bug fix: describe the symptom, the root cause, and the fix.
- Feature: describe the new behavior and why it was added.

If the PR is associated to a requirement or specification, list which 
requirements / specifications this pr is related to.
-->
Closes # ... by ...

### Review Level

<!--
Pick the tier that reflects the risk of this change. When in doubt, go one level up.

A high-risk change includes but is not limited to: 
- Changes that could break or alter existing user-facing behavior
- Changes that touch authentication, authorization, or permissions logic
- Changes that modify a shared API contract (added/removed/renamed fields, altered response shape)
- Changes that modify a shared utility, hook, context, or component used across the app
- Changes that require a paired backend, firmware, or infrastructure change to be deployed together
-->

- [ ] **Lightweight** - Isolated, low-risk change (copy/label edit, style tweak, documentation, single config value). 
No shared logic touched. Reviewer spot-check is enough.
- [ ] **Standard** - Typical bug fix or feature. Touches business logic or UI components but introduces no breaking 
changes. Full review expected.
- [ ] **Deep-dive** - High-risk change. Describe why this change is high-risk:
  

### AI assistance

<!--
Disclose how much code in this PR was AI-generated.
This helps reviewers calibrate how closely to read the logic.

As the PR Author, you must independently verify correctness, edge cases, and security implications before requesting a 
review. Do not request a review on unverified AI-generated code. 
-->

- [ ] **None**: All code written by the author without AI assistance
- [ ] **Partial**: Some code or logic was AI-generated. 
- [ ] **Majority**: Most of the implementation was AI-generated.

## Test plan

<!--
Document all coverage for this PR:
1) Unit tests created/updated for this change (include file/test names and status).
2) What testing you (the PR author) have already completed.
3) What a reviewer should run to verify and test edge cases.

Unit tests that cover this change should be included in this PR and should be passing before merge.

For each test, make it clear whether it was already run by the PR author and its result.

Be specific in your test description: include role (admin vs. non-admin), device, OS, or firmware target where relevant.
Check off each step as you confirm it locally before requesting review.

Reviewers should be able to follow this test plan to replicate success and validate any edge cases.
If the QMS 6.5.k Test plan contains tests that sufficiently cover the changes, it should be referenced here.

Example 1:
- [ ] Create a new quote as a Sales user — verify the sales rep selector appears and defaults to the current user
- [ ] Create a new quote as a Management user — verify the sales rep selector appears with no default (blank)
- [ ] Edit an existing quote — verify the saved sales rep is pre-selected in the dropdown
- [ ] Open a work order — verify the sales rep selector appears in the header next to Status
- [ ] Change the sales rep on a work order — verify the change saves immediately (auto-save on change)
- [ ] Verify that only users in the Sales group appear in the dropdown for both forms

Example 2:

| Test ID | Description                                                            | Pass Criteria                                                  | Passed? |
|---------|------------------------------------------------------------------------|----------------------------------------------------------------|---------|
| 1       | - Step 1<br/>- Step 2<br/>- Step 3                                     | X happens, B happens, C happens                                |         |
| WOQ-001 | See 1434-Classic Office Movers-QMS 6_5_k Test Plan-Milestone Release 1 |                                                                | yes     |
| 3       | Create a new quote as a sales user                                     | Verify sales rep selector appears and defaults to current user |         |
| 4       | Change sales rep on a work order                                       | Verify the changes are autosaved on change                     |         |

-->

| Test ID | Description | Pass Criteria | Test Status |
|---------|-------------|---------------|-------------|
| 1       |             |               |             |
| 2       |             |               |             |
| 3       |             |               |             |
| 4       |             |               |             |

## Screenshots / recordings

<!--
Relevant for any visible UI changes.
Attach before/after screenshots, a screen recording, just an after screenshot, etc.
Delete this section if the change is purely non-visual or the reviewer is expected to run the code to view the changes.
-->
**Before:**


**After:**

## Related PRs / dependencies

<!--
Cross-repo links, blocked-by, or depends-on. Delete if not applicable.
Format: org/repo#NNN — description
-->

## Reviewer notes

<!--
Anything that would help a reviewer: tricky areas to focus on, known limitations,
follow-up issues already filed, or explicit "I'm not sure about X, please advise."
Delete if nothing to add.
-->
