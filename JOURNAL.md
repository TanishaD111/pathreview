## Week 7 — Issue selection

**Issue link:** https://github.com/ascherj/pathreview/issues/57

**Issue title:** Add a mock GitHub API server for integration tests

**Tier:** [ ] Tier 1  [X] Tier 2  [ ] Tier 3

I can explain what the issue is in my own words as I have done below. I can see the files this code affects and I have read through these as well as what it is testing. I have also located all of the relevant files in the repo after I opened it on Visual Studio. I understand that it looks done when the GitHub tool tests can occur. 

This is my first open source contribution, but I would want to test myself and be able to give myself a challenge. I have looked through this issue in depth and I feel like I am willing to commit time and take this on. I am willing to look through multiple modules to see how everything interacts, so I am choosing a Tier 2 issue. 

I've found and read the specific code the issue references. I've read enough surrounding context that I can write a rough plan for the fix. I admittedly will likely have to look some things up, but I am confident I will be able to understand quickly and figure out what is needed. I have read the test file and know what to contribute. 

I've checked the issue comments and the ledger's Claims count, and I'm fine with how many others are on this issue. I've estimated the time this will take and I'm confident I can complete it before the Week 9 deadline. This issue has no open blockers or dependencies on other unresolved issues. 

**Problem summary:**
The `GitHubTool` in [agent/tools/github_tool.py](agent/tools/github_tool.py) calls the live GitHub REST API (`https://api.github.com`) to fetch repository metadata, so any
integration test that exercises it needs real network access and is subject to GitHub's rate limits and auth. As a result, those tests are skipped in CI, there is currently no
`tests/integration/test_github_tool.py` and no `tests/fixtures/github_responses/` directory, leaving the tool's request handling and error paths (404, 403/rate limit) untested by automation. The fix is to stand up a lightweight local mock HTTP server (`pytest-httpserver`) that serves canned JSON fixtures for GitHub endpoints and to point the tool's `base_url` at it, so the GitHub tool tests can run deterministically and offline in CI without hitting the real API.

**Branch name:** test/57-add-mock-github-api-server

**Setup confirmation:** [X] App runs locally at localhost:5173

**Cohort ledger:** [X] Issue added to cohort ledger


## Week 8 — Reproduction & solution planning

**Reproduction commit link:** https://github.com/TanishaD111/pathreview/commit/31b67ccc409eeeb4ae852756ba168b68e99e02ed

**Reproduction summary:**
Since this issue is to add in a functionality, there is nothing broken because of it. To reproduce it, there is nothing broken to show, but what I do observe is that the two files the review mentions (tests/integration/test_github_tool.py, tests/fixtures/github_responses/) just don't exist yet. Since these tests do not exist and the tool cannot be tested offline since its URL is hardcoded, the two files just arent there. I can see in the agent/tools/github_tool.py file, there is no way to point anything to a url link since the base url is https://api.github.com with no override in the constructor, so its 200/404/403 error paths can only be exercised against the real API, which is why they're skipped in CI. 

**PLAN.md link:** [X] This file is completed

**Blockers or open questions:**
n/a