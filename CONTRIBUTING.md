# Contributing Guidelines

This document covers the conventions for repositories, commits, pull requests, code review, and release. Following these 
conventions ensures consistency and compliance across Tangent's Quality Management System.

---

## Table of contents

1. [Repository setup](#repository-setup)
2. [Commit messages](#commit-messages)
3. [GitHub Issues](#github-issues)
4. [Opening a pull request](#opening-a-pull-request)
5. [Filling out the PR template](#filling-out-the-pr-template)
6. [Review process](#review-process)
7. [Merging](#merging)
8. [Release Process](#releasing)

---

## Repository setup

### Repository naming

Source code repositories follow this naming convention per QMS 5.0 Identification and Traceability:

```
XXXX-90-NNNN_ClientName_ModuleName
```

| Part         | Description                                                            |
|--------------|------------------------------------------------------------------------|
| `XXXX`       | Project number                                                         |
| `90`         | Tangent component ID for source code (see QMS-5.0.010)                 |
| `NNNN`       | Incremental module number within the project, starting at `0001`       |
| `ClientName` | Client name — may be shortened (e.g. `ClassicOffice`)                  |
| `ModuleName` | Short 1–2 word description of the module (e.g. `Frontend`, `Firmware`) |

**Example:** `1234-90-0001_CoolCompany_Frontend`

---

### Repository settings

All repositories must have the following configured:

**Branch protection:**
- Merge protection rules on `main` and `release` - direct pushes are not permitted.
- PRs require at least one approval before merge
- Never force-push to `main` or `release`

**CI/CD (when enabled):**
- Formatting checks must pass to merge
- Unit tests must pass to merge
- A simple build must complete to merge

Additional checks and rules can be configured as needed.

---

### Branch structure

Every repository requires two long-lived branches:

| Branch    | Purpose                                                   |
|-----------|-----------------------------------------------------------|
| `release` | Always points to the most recent formal release tag.      |
| `main`    | Active development branch. All feature work targets here. |

Feature branches are created off `main` (or off another feature branch for sequential work) and deleted after merge.

**Example hierarchy:**

```
release  (@ tag: v1.0.0)
main     (@ v1.0.0 + N commits)
  ├── lparker/34-storage-revamp
  │     └── lparker/45-temperature-sensor
  └── eeltherington/28-ui-updates
```

---

### Branch naming

```
<name>/<short-description>
<name>/<issue-number>-<short-description>
```

- **name** — your first initial + last name (e.g. `lparker`, `eeltherington`, `pkathol`)
- **issue-number** — the GitHub issue number this branch addresses
- **short-description** — brief lowercase hyphenated description of the work

Keep branch names lowercase with hyphens. No spaces or underscores. If a single branch addresses multiple issues with 
no single issue number, the issue number may be omitted in the branch name.

**Examples:**

```
lparker/247-work-order-state-refresh
eeltherington/214-add-work-order-notes
pkathol/34-boot-update-stm32f4
```

---

## GitHub Issues

Work is tracked using GitHub Issues. An individual issue represents a reasonably reviewable scope of work – large enough
to be meaningful to the project's progress, small enough to be understood in isolation without requiring extensive 
knowledge of the surrounding codebase.

Each issue should:

- Define the completion criteria and testing requirements for the work
- Link to the relevant requirements or specifications that provide acceptance criteria
- Be kept accurate and up to date as work progresses — current accuracy matters more than historical record

If the scope of an issue changes during implementation (e.g., work is deferred or requirements shift), Add comments to 
the original issue to reflect the modified scope and create a new issue to track any deferred or follow-up work.

External tasks tracked in other tools (e.g., Planner) that affect the codebase should have corresponding GitHub 
issues created to describe the work at the code level.

---

## Commit messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <short description>

<optional body>

<optional footer: Closes #NNN>
```

| Type       | When to use                                |
|------------|--------------------------------------------|
| `fix`      | Bug fix or patch                           |
| `feat`     | New feature or capability                  |
| `refactor` | Code restructuring without behavior change |
| `chore`    | Deps, config, tooling, CI                  |
| `docs`     | Documentation only                         |

**Examples:**

```
fix(dispatch): correct timezone parsing for calendar events

fix(auth): restrict break management to own records for non-admin users

feat(work-order): add notes field to quote and work order views

```

Guidelines:
- Subject line: 72 characters max, imperative mood ("add" not "added"), no period at end
- Reference issues in the footer/description: `Closes #241` or `Refs #230`
- One logical change per commit. Ideally squash WIP / cleanup commits before requesting review

---

## Opening a pull request

### Before you open

- [ ] Work has been committed and pushed regularly throughout development
- [ ] All relevant tests pass locally
- [ ] No unresolved merge conflicts

### PR title

Use the same format as commit messages:

```
fix(dispatch): correct timezone parsing for calendar events (closes #241)
```

- Issue number(s) in the title if space allows. This makes the PR list readable without opening each PR
- For multi-issue PRs: `fix: date format, filter, and comma fixes (closes #202, #203, #205, #206)`

---

## Filling out the PR template

Every section has a comment explaining when it is required vs. optional. Short guide:

| Section                        | Required?       | Notes                                                                        |
|--------------------------------|-----------------|------------------------------------------------------------------------------|
| **Summary**                    | Always          | Start with `Closes #NNN by...`, then one-sentence overview and detail.       |
| **Review level**               | Always          | Pick one tier; check any applicable Deep-dive sub-items. See guidance below. |
| **AI assistance**              | Always          | Pick one. "None" is fine — this is disclosure, not a judgment.               |
| **Test plan**                  | Always          | Steps with pass criteria. Fill in Test Status before requesting review.      |
| **Screenshots / recordings**   | When Applicable | Before/after, or delete if purely non-visual.                                |
| **Related PRs / dependencies** | When applicable | Cross-repo links, blocked-by.                                                |
| **Reviewer notes**             | When applicable | Tricky areas, known limitations, open questions.                             |

### Choosing a review level

The review level signals to your reviewer how much scrutiny this PR warrants.

**Lightweight** is appropriate when *all* the following are true:
- The change is fully isolated (one component, one config, one doc file, isolated change)
- No shared utilities, hooks, contexts, or components are touched
- No user-facing behavior changes beyond the specific targeted fix
- No auth, permissions, or API contract involved

**Standard** is the default for most PRs — typical bug fixes, new features, and refactors that don't touch auth or 
shared API code.

**Deep-dive** is required whenever the change could affect other parts of the system in ways that aren't obvious from 
the diff. Add details as to what causes this PR to be high risk, and use **Reviewer notes** to call out the riskiest 
areas.

When in doubt, go one level up.

### AI assistance disclosure

This field helps reviewers allocate their time — it is not a quality judgment.

- **Partial or Majority**: Before requesting review, walk through all AI-generated code yourself and verify it handles edge cases, error paths, and security constraints correctly. Reviewers will read AI-heavy code more closely, so make sure your test plan covers logic correctness, not just the happy path.
- Using AI assistance is fine and encouraged. The goal of this field is transparency.


### Test plan checklist quality

Bad: `- [ ] Test it`

Good:
```
- [ ] Log in as a non-admin employee — verify you can only see your own breaks
- [ ] Log in as an admin — verify you can see and manage all employees' breaks
- [ ] Create a break as non-admin, reload the page, confirm it persists
- [ ] Attempt to access `/breaks/other-employee-id` directly — confirm redirect or 403
```

For firmware, include:
- Target hardware tested on
- Test conditions
- Any automated test suite commands (`make test`, `pytest tests/`, etc.)

---

## Review process

### Requesting review

- Assign at least one reviewer before marking Ready for Review
- If your change touches an area owned by another developer, add the relevant person as an optional reviewer
- For cross-repo changes (e.g., frontend and backend), link both PRs in the **Related PRs** section of each

### Reviewer responsibilities

See [PULL_REQUEST_REVIEW_CHECKLIST.md](PULL_REQUEST_REVIEW_CHECKLIST.md) for the full reviewer checklist.

At a minimum, reviewers should confirm:
1. The summary matches the actual diff
2. The test plan is complete and was executed
3. No obvious issues/typos (auth checks, SQL injection, input validation, secrets in code)
4. Code follows project conventions (naming, file structure, existing patterns)

### Responding to feedback

- Resolve conversations only after addressing the comment (not before)
- If you disagree, reply with reasoning.
- Re-request review after pushing significant changes. 

---

## Merging

- **Squash and merge** is the default for feature branches (keeps `main` history clean)
- **Merge commit** for release branches or when preserving intermediate history matters
- **Never force-push to `main`**
- Delete the source branch after merge (GitHub does this automatically if configured)


**Post-approval changes:** Any changes made to a PR after it has been approved require a re-review. When requesting 
re-review, indicate within the PR comments the appropriate **Review level** for the new changes.


**The PR author is responsible for merging once approved.**

---

## Releasing

### Software versioning

All releases use semantic versioning: `Major.Minor.Patch`

| Component | When to increment                                                                                  |
|-----------|----------------------------------------------------------------------------------------------------|
| **Major** | Breaking change - the software is no longer compatible with connected devices or dependent systems |
| **Minor** | New features added in a backwards-compatible way                                                   |
| **Patch** | Backwards-compatible bug fixes only                                                                |

Internal working copies append a **Build** number: `Major.Minor.Patch.Build` (e.g. `1.2.1.16`). The build number is 
removed on formal release - `1.2.1.16` becomes `1.2.2` (or whichever increment is appropriate for the changes).

Binary image naming follows the same convention using component ID `91` for compiled source:

```
XXXX-91-NNNN_ClientName_ModuleName_Major-Minor-Patch
```

### Release process

Upon completion of validation testing and sign-off:

1. Create a GitHub release and add a version tag to the commit (e.g. `v1.2.1`)
2. Create a new release directory in PDM under the project's Software section for this version
3. Complete **Template QMS 6.5.c.8 Software Release Notes** and store it in the release directory
4. Copy the released compiled binary(s) to the release directory
5. Package all release artifacts and release notes into a compressed zip archive using the binary image naming convention
6. Notify affected stakeholders of the new release

### Release notes

Release notes must be copied into the GitHub release and stored with the released binaries in PDM. Include all 
applicable sections as per QMS 6.5.c.8:

- Product Overview: Version number, release date, ECO/Issue tracking number
- Date of release
- Reason for release
- New features
- Removed features
- Improvements / Enhancements
- Bug fixes
- Compatibility with other software or hardware versions
- Known issues

### Build documentation

Each release artifact must include documentation sufficient to reproduce the build from scratch on a clean machine:

- List of required software and their versions, with links to installers
- Any required libraries, modifications, or build system configuration
- Step-by-step instructions to produce the release artifact

This documentation is stored alongside the release artifacts in PDM.