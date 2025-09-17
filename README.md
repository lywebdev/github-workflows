# Workflow: Recreate PR under Token User

📂 Branch: [`workflows/pr-reassigning`](../../tree/workflows/pr-reassigning)  
📌 Related overview: see [Main README](../../blob/main/README.md)

---

## Purpose
This workflow ensures that all pull requests are created under a designated token user (`REVIEWER_TOKEN`).  
It closes the original PR if it was created by another user and recreates it under the token user, keeping reviewers and assignees consistent.

---

## Triggers
- `pull_request` events:
    - `opened`
    - `review_requested`

---

## Behavior
1. **Check `REVIEWER_TOKEN` secret**
    - If missing, the workflow stops.

2. **Validate PR**
    - Exits if PR is not open.
    - Exits if no reviewers are assigned.
    - Exits if PR was already created by the token user.
    - Exits if a duplicate PR already exists from the token user for the same branch.

3. **Close the original PR**
    - Marks the old PR as closed.

4. **Recreate the PR**
    - Creates a new PR under the token user with the same:
        - title
        - description (with a note referencing the old PR)
        - head and base branches
    - If creation fails, the original PR is reopened.

5. **Copy metadata**
    - Assignees are copied.
    - Reviewers are re-requested (excluding the token user).

6. **Add comments**
    - Notes are added to both old and new PRs about the recreation.

---

## Requirements
- **Repository secret:**
    - `REVIEWER_TOKEN` – GitHub token of the bot/token user.

---

## Notes
- Prevents duplicate PRs for the same branch under the token user.
- Ensures that all reviews flow through a single, consistent user.
- Works safely: if new PR creation fails, the original PR is restored.

