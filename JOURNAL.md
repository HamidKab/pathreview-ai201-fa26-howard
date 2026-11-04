## Unit 7 — Issue selection

**Issue link:** [[Issue Link](https://github.com/codepath/pathreview-ai201-fa26-howard/issues/67)]

**Issue title:** [Review creation does not verify profile ownership
]

**Tier:** [ ] Tier 1  [X] Tier 2  [ ] Tier 3
**Selection Notes:** I chose this issue because I understood the underlying problem of it easily. When I went to investigate where to find the bug I was able to easily point it out without the use of AI. I also believe that a tier 2 issue is perfect for me as I've worked on larger projects but not frequently enough to feel comfortable doing a tier 3 issue.

**Problem summary:**
[In 3–5 sentences, in your own words: what the issue is (not a copy-paste of
the title), what is currently broken or missing, and what a successful fix
would accomplish. Naming the part of the codebase it affects is helpful context.]
The API at POST/reviews passes the authenticated user ID to the function create_review(). Despite that, review_service.py ignores that argument when creating the review. The service creates a review without checking that the profile belongs to the current user making it inconsistent with other logics in the code.


**Branch name:** [fix/67-review-creation-auth]

**Setup confirmation:** [X] App runs locally at localhost:5173

**Cohort ledger:** [x] Issue added to cohort ledger