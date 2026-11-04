## Unit 7 — Issue selection

**Issue link:** [[Issue Link](https://github.com/codepath/pathreview-ai201-fa26-howard/issues/67)]

**Issue title:** [Review creation does not verify profile ownership
]

**Tier:** [ ] Tier 1  [X] Tier 2  [ ] Tier 3
**Selection Notes:** I chose this issue because I understood the underlying problem of it easily. When I went to investigate where to find the bug I was able to easily point it out without the use of AI. I also believe that a tier 2 issue is perfect for me as I've worked on larger projects but not frequently enough to feel comfortable doing a tier 3 issue.

**Problem summary:**
The API at POST/reviews passes the authenticated user ID to the function create_review(). Despite that, review_service.py ignores that argument when creating the review. The service creates a review without checking that the profile belongs to the current user making it inconsistent with other logics in the code. Postfix the outcome should look like the user_id being used in review_services.py to authenticate the profile to the user.

**How to verify (bug exists → bug fixed):**
- **Reproduce today:** Log in as User A and create a profile, then log in as User B and send `POST /reviews` with User A's `profile_id`. The request should fail but doesn't: it returns 200 with a `pending` review, and the background task starts processing User A's profile.
- **Expected after the fix:** The same request returns **404 "Profile not found"** and no review is created. I chose 404 over 403 because that's what `api/routes/profiles.py` already does. Its GET, PUT and DELETE endpoints all return 404 for both "not found" and "not owned by current user", so the API never confirms that someone else's profile exists. A random `profile_id` that doesn't exist should get the same 404.
- **Tests:** I checked for an existing `xfail(strict=True)` test tied to #67 (per `docs/CONTRIBUTING.md`) and there isn't one. The existing `test_create_review_*` tests in `tests/unit/test_review_service.py` only check that `db.add` and `commit` are called. So I'll add a test where `create_review` is called with a profile the user doesn't own and should not create a review, plus a route-level test that User B gets a 404. If I find an xfail marker for #67 later, I'll remove it as part of the fix.


**Branch name:** [fix/67-review-creation-auth]

**Setup confirmation:** [X] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger