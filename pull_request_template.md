## Summary

<!--
What changed and why. Lead with closing keywords, a one-sentence overview, then add detail.
- Bug fix: describe the symptom, the root cause, and the fix.
- Feature: describe the new behavior and why it was added.
- Multi-issue PR: use a sub-bullet per issue, e.g.:
  - ** Closes #202** — Fixed date format on invoices
  - ** Closes #203** — Removed trailing comma from totals row

For Firmware changes or changes involving some form of hardware, include the following details:
- **Breaking change for existing devices:** Yes / No
- **Target hardware:**  STM32F4, ESP32-S3, nRF52840, etc. 
- **Target hardware version:**  1.3.1
-->
Closes # ... by ...

## Test plan

<!--
List the steps a reviewer should take to verify this works.
Be specific: include role (admin vs. non-admin), device, OS, or firmware target where relevant.
Check off each step as you confirm it locally before requesting review.

Reviewers should then be able to follow this test plan to replicate. 
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
